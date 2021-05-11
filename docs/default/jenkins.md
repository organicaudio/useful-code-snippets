# Jenkins (pipeline)

- if you use a jenkins file it is called a multi branch pipeline (it uses the pipeline plugin)
- there is a imperative and a declarative pipeline syntax
- there is a vs code pipeline linter extension ['Jenkins Pipeline Linter Connector'](https://marketplace.visualstudio.com/items?itemName=janjoerke.jenkins-pipeline-linter-connector) which uses the jenkins build in pipeline linter: `http://<JENKINS:PORT>/pipeline-model-converter/validate`. You may need to configure the extension to ignore SSL errors.
- you can add (global) config files to the jenkins project like a settings.xml or property file with credentials
- if you use blue ocean you might not get the real error of a pipeline so you should open the console in classic view if stuff seems to be missing
- **do no use the variable name 'package' in jenkins file.**

## (declarative) pipeline examples

[official api documentation](https://www.jenkins.io/doc/book/pipeline/syntax/)

### define variables

- Use `environment` block 
    - below `pipeline` for all stages
    - below `stage` for one stage
- you can access the variables 
    - in `script` blocks like groovy variables
    - and within declarative syntax scope in strings with `"$VARIABLE_NAME"`


```groovy
pipeline {
    agent any
    environment {
        MY_GLOBAL_VARIABLE='i am global'
    }
    stages {
        stage('1'){
            steps {
                echo "$MY_GLOBAL_VARIABLE"
            }                    
        }
    }
}
```

### build java

- use bat or sh before unknown commands (depends on OS of jenkins agent)
- save artifact
- save test results

```groovy
pipeline {
    agent any
    stages {
        stage('build and save artifact'){
            steps {
                echo 'building project-a'
                sh 'mvn -B -DskipTests clean package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }                    
        }
        stage('test and save results') {
            steps { 
                echo 'testing project-a'
                sh 'mvn test'
                junit 'project-a/target/surefire-reports/*.xml' 
            }
        }
    }
}

```

### deploy with ssh

- use ssh pipeline step plugin 
    - [Github](https://github.com/jenkinsci/ssh-steps-plugin 
    - [Jenkins Doku](https://www.jenkins.io/doc/pipeline/steps/ssh-steps/)
- use stash/unstash to move stuff between stages
- if you define a variable like rmote you need to be in a script block
- when using `withCredentials` you can choose between `usernamePassword` or `sshUserPrivateKey`

**Prerequisite: The user must exist, needs to have the public key configured**

```groovy
pipeline {
    agent any
    stages {
        stage('build and save artifact'){
            steps {
                echo 'building project'
                sh 'mvn -B -DskipTests clean package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                stash includes: 'target/*.jar', name: 'project'

            }                    
        }
        stage('deploy artifact and run startSkript'){
            steps{
                echo 'deploy project'
                unstash 'project'
                // script block needed to define a variable 'remote'
                script {
                    // UUID (e.g. 42fb2924-4a89-43a4-8e96-1c2e0c61e446) of the jenkins credentials entity. If you only see the name of the credential you may use html devloper tools to find its uuid
                    // ssh credential for auth with private ssh key 
                    withCredentials([sshUserPrivateKey(credentialsId: '42fb2924-4a89-43a4-8e96-1c2e0c61e446', keyFileVariable: 'identity', passphraseVariable: 'passphrase', usernameVariable: 'userName')]) {

                    // ssh credential for password auth
                    //   usernameVariable([usernamePassword(credentialsId: '42fb2924-4a89-43a4-8e96-1c2e0c61e446', usernameVariable: 'userName', passwordVariable: 'password') {
                        
                        def remote = [:]
                        remote.user = 'jenkins' //probably not relevant when using ssh key
                        remote.identityFile = identity 
                        remote.passphrase = passphrase
                        remote.name = 'myhost'
                        remote.host = 'myhost.de'
                        remote.allowAnyHosts = true
                        // for password auth
                        //remote.user=userName
                        //remote.password=password
                        // or just:
                        // def remote = [user = 'jenkins', identityFile = identity,  passphrase = passphrase, name = 'myhost', host = 'myhost.de', allowAnyHosts = true]

                        println remote
                        sshCommand remote: remote, command: "pwd", sudo: "false"
                        // sshPut needs exact name match
                        sshPut remote: remote, from: 'target/app.jar', into: '.'
                        sshPut remote: remote, from: './start-app.sh', into: '.'
                        sshCommand remote: remote, command: "sh ./start-app.sh", sudo: "true"
                    }
                }
            }
        }
    }
}

```

### parallel build in monorepo

- parallel build
- use dir directive

```groovy
pipeline {
    agent any
    stages {
        stage('parallel stage'){
            parallel {
                stage('stage project-a') {      
                    stages {
                        stage('build project-a'){
                            steps {
                                dir('./project-a/') {
                                    echo 'building project-a'
                                }
                            }
                        }
                    }
                }
                stage('stage project-b') {      
                    stages {
                        stage('build project-b'){
                            steps {
                                dir('./project-b/') {
                                    echo 'building project-b'
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

### user interaction

#### yes/no prompt with timeout

- use `input` step to ask user for permission 
- set timeout option for stage so it will be finished if no user acknowledges the step

```groovy
stage('deploy'){
    when {
        branch: "master"
    }
    options{
        timeout(time:15, unit: 'MINUTES')
    }
    steps{
        input 'Deploy?'
        script {
            deploy("$environment", "stash-name" ,"spring-profile")
        }
    }
}

```

#### pipeline parameters

- add `parameters` block under `pipeline`
- asks user for input

Example from [official documentation](https://www.jenkins.io/doc/book/pipeline/syntax/#parameters)

```groovy
pipeline {
    agent any
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages {
        stage('Example') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }
    }
}
```

### define and use function (inline)

- You can define funtions below the `pipeline` block
- `def functionName(String paramExamle){}`
- function can be called in `steps` or `script` blocks depending on the used in the function: `functionName('myParam')`

```groovy
pipeline {
    agent any
    stages {
        stage('build and save artifact'){
            steps {
                build()
            }                    
        }
        stage('test and save results') {
            steps { 
               test()
            }
        }
    }
}

def build(){
    echo 'building project-a'
    sh 'mvn -B -DskipTests clean package'
    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
}

def test(){
    echo 'testing project-a'
    sh 'mvn test'
    junit 'project-a/target/surefire-reports/*.xml' 
}

```


### define and use function (library)

- [see](https://jaxenter.de/pipeline-jenkins-2-61568)

### create zip file


```groovy
pipeline {
    agent any
    stages {
        stage('zip whole workspace'){
            steps {
                zip zipFile: "../target.zip", archive: true, dir: "."
            }                    
        }
 
    }
}


```

### read xml

- use readFile file:'myFile.xml'
- **this might be prohibited by jenkins and need approval of an admin ("Manage jenkins-> In-process script approval")**
- [Examples for groovy XmlParser](https://groovy-lang.org/processing-xml.html)
- You should read xml file into string before processing it otherwise jenkins might throw exceptions


test.xml:

"""xml
<avatar>
    <name>Aang</name>
<avatar>

"""

```groovy
pipeline {
    agent any
    stages {
        stage('read from xml'){
            script {
                def xmlContentString = readFile("test.xml")
                // do not add root element (in this case avatar) to path
                println(getXmlSlurper(xmlContentString).name) //Aang
            }                    
        }
 
    }
}

@NonCPS
def getXmlSlurper(String xmlContentString){
    return new XmlSlurper().parseText(xmlContentString)
}
```

### remove old builds

- use buildDiscarder and logRotator api to remove old build artifacts
- [see](https://stackoverflow.com/questions/39542485/how-to-write-pipeline-to-discard-old-builds)

```groovy
pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))()
    }

      stage('build and save artifact'){
        steps {
            echo 'building project-a'
            sh 'mvn -B -DskipTests clean package'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }                    
    }

}

```

### clean jenkins workspace

- it may be that jenkins keep you workspace between two builds and you need to delete created folder
- A general solution is to skip default checkout mechanism and delete everything before checking out
- **this might slow down the build so you should consider to use custom delete logic in you pipeline**

```groovy
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                checkout scm
        }

    }
    stages {
        stage('do stuff'){
            steps {
                echo "do stuff"
            }                    
        }
 
    }
}
```