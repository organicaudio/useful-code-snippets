## Reference: List of iOS App URL Scheme Names & Paths for Shortcuts
### Author: 
### Source: https://ios.gadgethacks.com/how-to/always-updated-list-ios-app-url-scheme-names-paths-for-shortcuts-0184033/
#### Saved on: 2021-03-19, 15:52

If you've ever customized your app icons or played around with Shortcuts (previously called Workflow), you probably know how important URL scheme names are. Nearly all iOS apps assign themselves one of these names, and you need to know them if you want to add custom icons to your home screen or create a Shortcuts workflow that opens an app on your iPhone up.
Finding the URL scheme name, also known as a URI scheme, for a particular app is not easy. First, you have to download the IPA file for the app — a difficult task since the iTunes 12.7 update removed iOS apps from it. When you finally find the IPA, you have to turn it into a ZIP file, show the contents of the app package, then hunt for the specific PLIST file that contains the URL schemes. It's a lot of work.

This example shows the URL schemes for VSCO in one of its PLIST files.
You can take some of the work out of digging through IPAs by downloading the extract-scheme-url.sh script on your Mac and running bash extract-scheme-url.sh AppName.ipa in a terminal window in the directory where those files are.
As for the IPAs, the easiest way to download IPA files is to use Apple Configurator 2. After signing in and connecting your iPhone, you can view and update apps that need it. Any apps you update this way will be stored temporarily in an Apple Config folder in the "Group Containers" folder in your user library. But it's still a lot of work and requires that the app you need has an update you can apply.
	•	More Info: How to Download IPA Files for the iOS Apps on Your iPhone
If all you want to do is create a custom app icon or open the Netflix app from a workflow you're toying with, we'll try to make things as easy as possible for you by listing below all of the URL scheme names for apps that we know of right now. Also, when we come across them, we'll not only include the "open" schemes, but some deep links URL schemes to jump to specific tasks inside an app.
While the list below may seem small considering there are over 2 million apps in the App Store, it's a work in progress, and we'll keep adding to it as we discover more URL schemes for popular apps and games on iPhone.
	•	Don't Miss: How to Customize iOS App Icons Without Jailbreaking Your iPhone
Quick Guide to Using URL Schemes in Shortcuts
Before moving on to the list, let's do a quick lesson on using URL schemes in the Shortcuts app. When iOS 13 came out, Shortcuts removed the need to use any "open" URL schemes since it added a new "Open App" script that will let you choose any app on your iPhone. That makes things so much easier.
Still, if you prefer the old way, want to use deep links, or want to know the base URL scheme to investigate for possible deep links, check out the first screenshot below. You input the URL scheme into the "URL" web action, then use the "Open URLs" web action below it to perform the task. It's essentially the same as using the "Open App" script seen in the second screenshot below.


URL schemes are more handy for deep links where you want to perform a specific action. As seen below, you can see I'm opening up the "Customize Controls" settings in the "Control Center" preferences.


URL Schemes for Popular iOS Apps & Services
Any ones below without anything after the :// are just schemes to open the apps up, while ones with information after the :// are for performing "deep link" specific actions within the apps. Also, while all of the below include the :// in them, most can be used with just : instead of with the // symbols.
Keep in mind that developers may change the URL schemes for their apps at any time. Apple has done so for certain iOS services, such as links to specific settings, with each new iOS update (iOS 11, iOS 12, iOS 13, iOS 14, etc.). Some URL schemes you can probably even guess since a lot just use their app's name as the scheme name. Trial and error!
Schemes for the Settings app (listed below) are merely paths to Settings menus. Apple restricts schemes from being able to toggle switches on and off, select different features from a list, and so on. It does so for security purposes, so that runaway apps or shortcuts don't alter your settings without you realizing it.
Also, anything below that starts with fb*:// are Facebook deep links that should work whether or not you have Facebook installed on your device. Since they don't always work as expected, we've only included them in the list below if they had no other URL scheme name. Otherwise, fb*:// schemes are omitted.
Apple-Branded Apps & Services
	•	App Store:
Open = itms-apps://itunes.apple.com

Open account settings = itms-ui://

Open app = itms-apps://itunes.apple.com/app/id

Search = itms-apps://search.itunes.apple.com/WebObjects/MZSearch.woa/wa/search?media=software&term=YourQuery

Top charts = itms-apps://itunes.apple.com/WebObjects/MZStore.woa/wa/viewTop?genreId=36&popId=30
	•	Apple Store:
Open = applestore://
       applestore-sec://
       applestore-alipay://
	•	Books:
Open = ibooks://
       itms-books://
       itms-bookss://
	•	Calculator:
Open = calc://
	•	Calendar:
Open = calshow://
       x-apple-calevent://

Add calendar = webcal://SuscribeLinkForTheCalendar
	•	Clips:
Open = clips://
	•	Clock:
Open = clock-alarm://
       clock-sleep-alarm://
       clock-stopwatch://
       clock-timer://
       clock-worldclock://
	•	Contacts:
Open = contact://
	•	Diagnostics:
Open = diagnostics://
       diags://
	•	FaceTime:
Start audio call = facetime-audio://TheirPhoneNumberOrEmailAddress
                   facetime-audio-prompt://TheirPhoneNumberOrEmailAddress

Start video call = facetime://TheirPhoneNumberOrEmailAddress
                   facetime-prompt://TheirPhoneNumberOrEmailAddress
	•	Feedback:
Open = applefeedback://
	•	Files:
Open = shareddocuments://

Connect to server = smb://
	•	Find My:
Open = findmy://

Show items list: findmy://items  (iOS 14.3 and later)
	•	Find My Friends:
Open = findmyfriends://
       fmf1://
       grenada://
	•	Find My iPhone:
Open = fmip1://
	•	Game Center:
Open = gamecenter://  (unverified, pre-iOS 11)
       itms-gc://  (unverified, pre-iOS 11)
       itms-gcs://  (unverified, pre-iOS 11)
	•	GarageBand:
Open = garageband://
	•	Health:
Open = x-apple-health://
       x-argonaut-app://
	•	Home:
Open = x-hm://
	•	iBooks:
Open = ibooks://
       itms-books://
       itms-bookss://
	•	iCloud Drive:
Open = appleiclouddrive://  (unverified, pre-iOS 11)
	•	iMovie:
Open = imovie://
	•	iTunes Remote:
Open = remote://
	•	iTunes Store:
Open = itms://
       itmss://
	•	iTunes U:
Open = itms-itunesu://
	•	Maps:
Open = map://
       maps://
       mapitem://
	•	Mail:
Open = message://

Start draft with recipient = mailto:TheirEmailAddress

Start draft with recipient, cc = mailto:TheirEmailAddress?cc=TheirEmailAddress

Start draft with recipient, bcc = mailto:TheirEmailAddress?bcc=TheirEmailAddress

Start draft with recipient, subject = mailto:TheirEmailAddress&subject=Your%20Subject%20Text

Start draft with recipient, body = mailto:TheirEmailAddress&body=Your%20Body%20Text

Start draft with recipient, CC, BCC, subject, body = mailto:TheirEmailAddress?cc=TheirEmailAddress?bcc=TheirEmailAddress&subject=Your%20Subject%20Text&body=Your%20Body%20Text

[You can make other combinations above using the above identifiers]
	•	Messages:
Open = messages://

Open App Store = itms-messages://

Open new text = sms://

Open new text for contact = sms://TheirPhoneNumber
                            sms-private://TheirPhoneNumber
	•	Music:
Open = music://
       musics://
       audio-player-event://

Open radio = itsradio://  (unverified)
             itsradios://  (unverified)
             itunesradio://  (unverified)
             itunesradios://  (unverified, just opens Music)
	•	News:
Open = applenews://
       applenewss://
	•	Notes:
Open = mobilenotes://
	•	Phone:
Open = mobilephone://

Call contact = tel://TheirPhoneNumber
               telprompt://TheirPhoneNumber

Show favorites = mobilephone-favorites://

Show recents = mobilephone-recents://

Show voicemail = vmshow://

	•	Photos:
Open = photos-redirect://

	•	Podcasts:
Open = pcast://  (goes to "Can't connect right now" screen by itself)
       podcasts://  (goes to "Can't connect right now" screen by itself)
       itms-pcast://  (goes to "Can't connect right now" screen by itself)
       itms-pcasts://  (goes to "Can't connect right now" screen by itself)
       itms-podcast://  (goes to "Can't connect right now" screen by itself)
       itms-podcasts://    (goes to "Can't connect right now" screen by itself)

Add feed by URL = feed://
                  podcast://

Add specific feed by URL = feed://TheUrlOfTheFeed
                           podcast://TheUrlOfTheFeed
	•	Reminders:
Open = x-apple-reminder://
       x-apple-reminderkit://
	•	Safari:
Search = x-web-search://

Open FTP file = ftp://LocationToFileOnFtpServer

Open HTTP site = http://WebsiteURL

Open HTTPS site = https://WebsiteURL
	•	Settings:
Open = App-prefs://
       App-prefs:
       prefs://
       prefs:
       prefs:root

Accessibility = SEE NEXT SECTION FOR ACCESSIBILITY SCHEMES

Apple Pencil (iPad-only) = prefs:root=Pencil

App Store = prefs:root=STORE
App Store ⇾ App Downloads = prefs:root=STORE&path=App%20Downloads
App Store ⇾ Video Autoplay = prefs:root=STORE&path=Video%20Autoplay

Battery = prefs:root=BATTERY_USAGE
Battery ⇾ Battery Health (iPhone-only) = prefs:root=BATTERY_USAGE&path=BATTERY_HEALTH

Bluetooth = prefs:root=Bluetooth

Books = prefs:root=IBOOKS

Calendar = prefs:root=CALENDAR
Calendar ⇾ Alternate Calendars = prefs:root=CALENDAR&path=Alternate%20Calendars
Calendar ⇾ Default Alert Times = prefs:root=CALENDAR&path=Default%20Alert%20Times
Calendar ⇾ Default Calendar = prefs:root=CALENDAR&path=Default%20Calendar
Calendar ⇾ Sync = prefs:root=CALENDAR&path=Sync

Camera = prefs:root=CAMERA
Camera ⇾ Record Slo-mo = prefs:root=CAMERA&path=Record%20Slo-mo
Camera ⇾ Record Video = prefs:root=CAMERA&path=Record%20Video

Cellular = prefs:root=MOBILE_DATA_SETTINGS_ID
Cellular ⇾ Cellular Data Options = prefs:root=MOBILE_DATA_SETTINGS_ID&path=CELLULAR_DATA_OPTIONS
Cellular ⇾ Low Data Mode = prefs:root=MOBILE_DATA_SETTINGS_ID&path=CELLULAR_DATA_OPTIONS#Low%20Data%20Mode
Cellular ⇾ App Data Usage = prefs:root=MOBILE_DATA_SETTINGS_ID#APP_DATA_USAGE

Compass = prefs:root=COMPASS

Contacts = prefs:root=CONTACTS

Control Center = prefs:root=ControlCenter
Control Center ⇾ Customize Controls = prefs:root=ControlCenter&path=CUSTOMIZE_CONTROLS

Display = prefs:root=DISPLAY
Display ⇾ Auto Lock = prefs:root=DISPLAY&path=AUTOLOCK
Display ⇾ Text Size = prefs:root=DISPLAY&path=TEXT_SIZE

Do Not Disturb = prefs:root=DO_NOT_DISTURB
Do Not Disturb ⇾ Allow Calls From = prefs:root=DO_NOT_DISTURB&path=Allow%20Calls%20From

Emergency SOS = prefs:root=EMERGENCY_SOS

Exposure Notifications = prefs:root=EXPOSURE_NOTIFICATION

Face ID = prefs:root=PASSCODE

FaceTime = prefs:root=FACETIME

Game Center = prefs:root=GAMECENTER

General = prefs:root=General
General ⇾ About = prefs:root=General&path=About
General ⇾ About ⇾ Certificate Trust Settings = prefs:root=General&path=About/CERT_TRUST_SETTINGS
General ⇾ AirDrop = prefs:root=General&path=AIRDROP_LINK
General ⇾ AirPlay & Handoff = prefs:root=General&path=CONTINUITY_SPEC
General ⇾ AirPlay & Handoff ⇾ Handoff = prefs:root=General&path=CONTINUITY_SPEC#CONTINUITY
General ⇾ AirPlay & Handoff ⇾ Automatically AirPlay to TVs = prefs:root=General&path=CONTINUITY_SPEC#AIRPLAY_TO_TV
General ⇾ AirPlay & Handoff ⇾ Transfer to HomePod = prefs:root=General&path=CONTINUITY_SPEC#TRANSFER_TO_HOMEPOD
General ⇾ Background App Refresh = prefs:root=General&path=AUTO_CONTENT_DOWNLOAD
General ⇾ CarPlay = prefs:root=General&path=CARPLAY
General ⇾ Date & Time = prefs:root=General&path=DATE_AND_TIME
General ⇾ Dictionary = prefs:root=General&path=DICTIONARY
General ⇾ Home Button = prefs:root=General&path=HOME_BUTTON
General ⇾ iPhone Storage = prefs:root=General&path=STORAGE_MGMT#MANAGE
General ⇾ iPhone Storage ⇾ Offload Unused Apps = prefs:root=General&path=STORAGE_MGMT#OFFLOAD
General ⇾ Keyboard = prefs:root=General&path=Keyboard
General ⇾ Keyboard ⇾ Keyboards = prefs:root=General&path=Keyboard/KEYBOARDS
General ⇾ Keyboard ⇾ One Handed Keyboard = prefs:root=General&path=Keyboard/ReachableKeyboard
General ⇾ Keyboard ⇾ Text Replacement = prefs:root=General&path=Keyboard/USER_DICTIONARY
General ⇾ Language & Region = prefs:root=General&path=INTERNATIONAL
General ⇾ Legal & Regulatory = prefs:root=General&path=LEGAL_AND_REGULATORY
General ⇾ Multitasking (iPad-only) = prefs:root=General&path=MULTITASKING
General ⇾ Multitasking (iPad-only) = prefs:root=General#Multitasking_Gesture_Switch
General ⇾ Picture in Picture = prefs:root=General&path=PiP_SPEC
General ⇾ Profiles = prefs:root=General&path=ManagedConfigurationList
General ⇾ Regulatory = prefs:root=General&path=REGULATORY
General ⇾ Reset = prefs:root=General&path=Reset
General ⇾ Reset ⇾ Reset All Settings = prefs:root=General&path=Reset#settingsErase
General ⇾ Reset ⇾ Erase All Content and Settings = prefs:root=General&path=Reset#fullErase
General ⇾ Reset ⇾ Reset Network Settings = prefs:root=General&path=Reset#RESET_NETWORK_LABEL
General ⇾ Reset ⇾ Reset All Cellular Plans = prefs:root=General&path=Reset#cellularErase
General ⇾ Reset ⇾ Subscriber Services = prefs:root=General&path=Reset#SUBSCRIBER_SERVICES_ID
General ⇾ Reset ⇾ Reset Keyboard Dictionary = prefs:root=General&path=Reset#RESET_KEYBOARD_DICTIONARY_LABEL
General ⇾ Reset ⇾ Reset Home Screen Layout = prefs:root=General&path=Reset#RESET_ICONS_LABEL
General ⇾ Reset ⇾ Reset Location & Privacy = prefs:root=General&path=Reset#RESET_PRIVACY_LABEL
General ⇾ Shut Down = prefs:root=General#SHUTDOWN_LABEL
General ⇾ Software Update = prefs:root=General&path=SOFTWARE_UPDATE_LINK
General ⇾ Trackpad & Mouse (iPad-only) = prefs:root=General&path=POINTERS
General ⇾ TV Out = prefs:root=General&path=TV_OUT
General ⇾ Use Side Switch To = prefs:root=General#Rotation_Switch_Action_Group
General ⇾ VPN = prefs:root=General&path=VPN
General (Unknown Path) = prefs:root=General&path=NFC_LINK

Health = prefs:root=HEALTH

iCloud = prefs:root=CASTLE
iCloud Backup = prefs:root=CASTLE&path=BACKUP

Mail = prefs:root=MAIL
Mail ⇾ Blocked = prefs:root=MAIL&path=Blocked
Mail ⇾ Blocked Sender Options = prefs:root=MAIL&path=Blocked%20Sender%20Options
Mail ⇾ Default Account = prefs:root=MAIL&path=Default%20Account
Mail ⇾ Include Attachments with Replies = prefs:root=MAIL&path=Include%20Attachments%20with%20Replies
Mail ⇾ Increase Quote Level = prefs:root=MAIL&path=Increase%20Quote%20Level
Mail ⇾ Mark Addresses = prefs:root=MAIL&path=Mark%20Addresses
Mail ⇾ Muted Thread Action = prefs:root=MAIL&path=Muted%20Thread%20Action
Mail ⇾ Notifications = prefs:root=MAIL&path=NOTIFICATIONS
Mail ⇾ Preview = prefs:root=MAIL&path=Preview
Mail ⇾ Signature = prefs:root=MAIL&path=Signature
Mail ⇾ Swipe Options = prefs:root=MAIL&path=Swipe%20Options

Maps = prefs:root=MAPS
Maps ⇾ Driving & Navigation = prefs:root=MAPS&path=Driving%20%26%20Navigation
Maps ⇾ Transit = prefs:root=MAPS&path=Transit

Measure = prefs:root=MEASURE

Messages = prefs:root=MESSAGES

Music = prefs:root=MUSIC
Music ⇾ Cellular Data = prefs:root=MUSIC&path=com.apple.Music:CellularData
Music ⇾ EQ = prefs:root=MUSIC&path=com.apple.Music:EQ
Music ⇾ Optimize Storage = prefs:root=MUSIC&path=com.apple.Music:OptimizeStorage
Music ⇾ Volume Limit = prefs:root=MUSIC&path=com.apple.Music:VolumeLimit

News = prefs:root=NEWS

Notes = prefs:root=NOTES
Notes ⇾ Access Notes from Lock Screen = prefs:root=NOTES&path=Access%20Notes%20from%20Lock%20Screen
Notes ⇾ Default Account = prefs:root=NOTES&path=Default%20Account
Notes ⇾ Lines & Grids = prefs:root=NOTES&path=Lines%20%26%20Grids
Notes ⇾ New Notes Start With = prefs:root=NOTES&path=New%20Notes%20Start%20With
Notes ⇾ Password = prefs:root=NOTES&path=Password
Notes ⇾ Sort Checked Items = prefs:root=NOTES&path=Sort%20Checked%20Items
Notes ⇾ Sort Notes By = prefs:root=NOTES&path=Sort%20Notes%20By

Notifications = prefs:root=NOTIFICATIONS_ID
Notifications ⇾ Siri Suggestions = prefs:root=NOTIFICATIONS_ID&path=Siri%20Suggestions

Passwords & Accounts = prefs:root=ACCOUNTS_AND_PASSWORDS
Passwords & Accounts ⇾ Fetch New Data = prefs:root=ACCOUNTS_AND_PASSWORDS&path=FETCH_NEW_DATA
Passwords & Accounts ⇾ Add Account = prefs:root=ACCOUNTS_AND_PASSWORDS&path=ADD_ACCOUNT

Personal Hotspot = prefs:root=INTERNET_TETHERING
Personal Hotspot ⇾ Family Sharing = prefs:root=INTERNET_TETHERING&path=Family%20Sharing
Personal Hotspot ⇾ Wi-Fi Password = prefs:root=INTERNET_TETHERING&path=Wi-Fi%20Password

Phone = prefs:root=Phone

Photos = prefs:root=Photos

Privacy: prefs:root=Privacy
Privacy ⇾ Contacts = prefs:root=Privacy&path=CONTACTS
Privacy ⇾ Calendars = prefs:root=Privacy&path=CALENDARS
Privacy ⇾ Camera = prefs:root=Privacy&path=CAMERA
Privacy ⇾ Location Services = prefs:root=Privacy&path=LOCATION
Privacy ⇾ Microphone = prefs:root=Privacy&path=MICROPHONE
Privacy ⇾ Motion = prefs:root=Privacy&path=MOTION
Privacy ⇾ Photos = prefs:root=Privacy&path=PHOTOS
Privacy ⇾ Reminders = prefs:root=Privacy&path=REMINDERS
Privacy ⇾ Speech Recognition = prefs:root=Privacy&path=SPEECH_RECOGNITION

Reminders = prefs:root=REMINDERS
Reminders ⇾ Default List = prefs:root=REMINDERS&path=DEFAULT_LIST

Ringtone = prefs:root=Sounds&path=Ringtone

Safari = prefs:root=SAFARI
Safari ⇾ Camera = prefs:root=SAFARI&path=Camera
Safari ⇾ Close Tabs = prefs:root=SAFARI&path=Close%20Tabs
Safari ⇾ Content Blockers = prefs:root=SAFARI&path=Content%20Blockers
Safari ⇾ Downloads = prefs:root=SAFARI&path=DOWNLOADS
Safari ⇾ Location = prefs:root=SAFARI&path=Location
Safari ⇾ Microphone = prefs:root=SAFARI&path=Microphone
Safari ⇾ Page Zoom = prefs:root=SAFARI&path=Page%20Zoom
Safari ⇾ Reader = prefs:root=SAFARI&path=Reader
Safari ⇾ Request Desktop Website = prefs:root=SAFARI&path=Request%20Desktop%20Website

Screen Time = prefs:root=SCREEN_TIME
Screen Time ⇾ Always Allowed = prefs:root=SCREEN_TIME&path=ALWAYS_ALLOWED
Screen Time ⇾ App Limits = prefs:root=SCREEN_TIME&path=APP_LIMITS
Screen Time ⇾ Communication Limits = prefs:root=SCREEN_TIME&path=COMMUNICATION_LIMITS
Screen Time ⇾ Content & Privacy Restrictions = prefs:root=SCREEN_TIME&path=CONTENT_PRIVACY
Screen Time ⇾ Downtime = prefs:root=SCREEN_TIME&path=DOWNTIME

Shortcuts = prefs:root=SHORTCUTS
Shortcuts ⇾ iCloud Sync = prefs:root=SHORTCUTS#WFCloudKitSyncEnabled
Shortcuts ⇾ iCloud Sync = prefs:root=SHORTCUTS#WFCloudKitSyncOrderEnabled
Shortcuts ⇾ Legal Notices = prefs:root=SHORTCUTS&path=Legal%20Notices

Siri & Search = prefs:root=SIRI
Siri & Search ⇾ Allow Siri When Locked = prefs:root=SIRI#ASSISTANT_LOCK_SCREEN_ACCESS
Siri & Search ⇾ Language = prefs:root=SIRI&path=LANGUAGE_ID
Siri & Search ⇾ Siri Voice = prefs:root=SIRI&path=VOICE_ID
Siri & Search ⇾ Siri Responses = prefs:root=SIRI&path=VOICE_FEEDBACK_ID
Siri & Search ⇾ My Information = prefs:root=SIRI&path=MY_INFO
Siri & Search ⇾ Suggestions in Search = prefs:root=SIRI#Suggestions%20in%20Search
Siri & Search ⇾ Suggestions while Searching = prefs:root=SIRI#Suggestions%20while%20Searching
Siri & Search ⇾ Suggestions in Look Up = prefs:root=SIRI#Suggestions%20in%20Look%20Up
Siri & Search ⇾ Suggestions on Lock Screen = prefs:root=SIRI#Suggestions%20on%20Lock%20Screen
Siri & Search ⇾ Suggestions on Home Screen = prefs:root=SIRI#Suggestions%20on%20Home%20Screen
Siri & Search ⇾ Suggestions when Sharing = prefs:root=SIRI#Suggestions%20when%20Sharing

Sounds = prefs:root=Sounds

Stocks = prefs:root=STOCKS
Stocks ⇾ Privacy = prefs:root=STOCKS#Privacy
Stocks ⇾ Reset Identifier = prefs:root=STOCKS#reset_identifier

TV = prefs:root=TVAPP
TV ⇾ Use Cellular Data = prefs:root=TVAPP#com.apple.videos%3AVideosUseCellularDataEnabledSetting
TV ⇾ Playback Quality = prefs:root=TVAPP#com.apple.videos%3APlaybackQualityGroup
TV ⇾ Video Definition = prefs:root=TVAPP&path=com.apple.videos%3APreferredPurchaseResolution
TV ⇾ Home Sharing = prefs:root=TVAPP#com.apple.videos%3AHomeSharingFooter

TV Provider = prefs-tvprovider://

Voice Memos = prefs:root=VOICE_MEMOS

VPN = prefs:root=General&path=VPN

Wallet = prefs:root=PASSBOOK

Wallpaper = prefs:root=Wallpaper

Wi-Fi = prefs:root=WIFI
	•	Settings (Accessibility):
Settings ⇾ Accessibility:
─────────────────────────
prefs:root=ACCESSIBILITY
prefs:root=ACCESSIBILITY_DESCRIPTION
prefs:root=ACCESSIBILITY_KEYWORDS
prefs:root=ACCESSIBILITY#VISION
prefs:root=ACCESSIBILITY#MOBILITY_HEADING
prefs:root=ACCESSIBILITY#HEARING_HEADING
prefs:root=ACCESSIBILITY#GENERAL_HEADING

Settings ⇾ Accessibility ⇾ VoiceOver:
─────────────────────────────────────
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#VoiceOverTouchEnabled
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#SpeakingRate
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#Speech
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Speech#DialectCell
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#Verbosity
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity#voiceOverPunctuationGroup
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity#speakTableHeader
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity#voiceOverMediaDescriptions
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity/voiceOverMediaDescriptions#mdOff
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity/voiceOverMediaDescriptions#mdSpeech
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity/voiceOverMediaDescriptions#mdBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Verbosity/voiceOverMediaDescriptions#mdSpeechAndBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#Braille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#BrailleDisplayOutput
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayOutput#SixDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayOutput#EightDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayOutput#ContractedBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#BrailleDisplayInput
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayInput#SixDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayInput#EightDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayInput#ContractedBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleDisplayInput#GRADE2_AUTO_TRANSLATE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#BrailleGesturesInput
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleGesturesInput#SixDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleGesturesInput#EightDotBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleGesturesInput#ContractedBraille
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/BrailleGesturesInput#SHOULD_REVERSE_DOTS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#tableIdentifier
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/tableIdentifier#ADD_NEW_BRAILLE_LANGUAGE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#STATUS_CELL
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/STATUS_CELL#STATUS_CELL_POSITION
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/STATUS_CELL#STATUS_CELL_LEFT
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/STATUS_CELL#STATUS_CELL_RIGHT
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/STATUS_CELL#StatusCellGeneral
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille/STATUS_CELL#StatusCellTextStyle
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#ALWAYS_USE_NEMETH
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#SHOW_SW_KEYBOARD
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#AUTO_TURN_PAGES
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Braille#WORD_WRAP
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#Audio
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Audio#AUDIO_DUCKING
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Audio#ROUTE_TO_SPEAKER
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Audio#ROUTE_TO_HDMI
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#CUSTOMIZE_COMMANDS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#Activities
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Activities#Programming
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/Activities#New
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#WebRotor
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#ROTOR_ACTIONS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/ROTOR_ACTIONS#EDIT_APPS_ACTION
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#TypingOptions
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions#TYPING_MODE_TITLE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/TYPING_MODE_TITLE#TYPING_MODE_STANDARD
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/Typing%20Style#TYPING_MODE_TOUCH_TYPING
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/Typing%20Style#TYPING_MODE_DIRECT_TOUCH
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions#PHONETICS_TITLE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/PHONETICS_TITLE#PHONETICS_OFF
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/PHONETICS_TITLE#PHONETICS_SPEAK_AFTER_DELAY
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/PHONETICS_TITLE#PHONETICS_SPEAK_EXCLUSIVELY
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions#TYPING_FEEDBACK
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions#MODIFIER_KEYS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/MODIFIER_KEYS#VO_MODIFIER_KEY_CONTROL_OPTIONS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions/MODIFIER_KEYS#VO_MODIFIER_KEY_CAPS_LOCK
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/TypingOptions#KEYBOARD_TIMING_TIMEOUT
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#SPEAK_NOTIFICATIONS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#IncludeUnlabeledImages
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/IncludeUnlabeledImages#NAV_IMG_ALWAYS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/IncludeUnlabeledImages#NAV_IMG_W_DESCRIPTIONS
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/IncludeUnlabeledImages#NAV_IMG_NEVER
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#CursorStyle
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#CaptionPanel
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE#DOUBLE_TAP_INTERVAL_TITLE
prefs:root=ACCESSIBILITY&path=VOICEOVER_TITLE/DOUBLE_TAP_INTERVAL_TITLE#NumericalPreferencePickerGroupIdentifier

Settings ⇾ Accessibility ⇾ Zoom:
────────────────────────────────
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomTouchEnabled
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomShouldFollowFocus
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomAlwaysUseWindowZoomForTyping
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomKeyboardShortcuts
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomEnableKeyboardShortcuts
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutAdjustZoomLevel
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutToggleZoom
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutPanZoom
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutResizeZoomWindow
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutSwitchZoomMode
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutTempToggleZoom
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomKeyboardShortcuts#ZoomKeyboardShortcutScrollWheel
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomSlug
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomLensMode
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomLensMode#Fullscreen
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE/ZoomLensMode#Window
prefs:root=ACCESSIBILITY&path=ZOOM_TITLE#ZoomFactorGroup

Settings ⇾ Accessibility ⇾ Magnifier:
─────────────────────────────────────
prefs:root=ACCESSIBILITY&path=MAGNIFIER_TITLE
prefs:root=ACCESSIBILITY&path=MAGNIFIER_TITLE#MagnifierEnabled
prefs:root=ACCESSIBILITY&path=MAGNIFIER_TITLE#AutoBrightness

Settings ⇾ Accessibility ⇾ Display & Text Size:
───────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#ENHANCE_TEXT_LEGIBILITY
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#LARGER_TEXT
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#BUTTON_SHAPES
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#OnOffLabels
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#REDUCE_TRANSPARENCY
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#TEXT_COLORS_DARKEN
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#DIFFERENTIATE_WITHOUT_COLOR
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#SMART_INVERT
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#CLASSIC_INVERT
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#DISPLAY_FILTER_COLOR
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT/DISPLAY_FILTER_COLOR#FILTER_COLOR_ENABLED
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#WHITE_POINT
prefs:root=ACCESSIBILITY&path=DISPLAY_AND_TEXT#AUTO_BRIGHTNESS

Settings ⇾ Accessibility ⇾ Motion:
──────────────────────────────────
prefs:root=ACCESSIBILITY&path=MOTION_TITLE
prefs:root=ACCESSIBILITY&path=MOTION_TITLE#REDUCE_MOTION_ID
prefs:root=ACCESSIBILITY&path=MOTION_TITLE#ReduceMotionAutoplayMessagesEffects
prefs:root=ACCESSIBILITY&path=MOTION_TITLE#ReduceMotionAutoplayVideoPreviews

Settings ⇾ Accessibility ⇾ Spoken Content:
──────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#QUICK_SPEAK_TITLE
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#SpeakThisEnabled
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#SpeechController
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/SpeechController#CustomizeMouseButtons
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#QuickSpeakHighlight
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#TypingFeedback
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#TYPING_FEEDBACK_HEADER
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#LETTER
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#PhoneticFeedback
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#WORD_FEEDBACK
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#SPEAK_AUTOCORRECTIONS
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE/TypingFeedback#QUICKTYPE_WORD_FEEDBACK
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#QuickSpeakAccents
prefs:root=ACCESSIBILITY&path=SPEECH_TITLE#QuickSpeakRateGroup

Settings ⇾ Accessibility ⇾ Audio Descriptions:
──────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=DESCRIPTIVE_VIDEO
prefs:root=ACCESSIBILITY&path=DESCRIPTIVE_VIDEO#DESCRIPTIVE_VIDEO_SETTING

Settings ⇾ Accessibility ⇾ Touch:
─────────────────────────────────
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#AIR_TOUCH_TITLE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#EnableAssistiveTouchSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#AssistiveTouchCustomize
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/AssistiveTouchCustomize#ASTStepperCell
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/AssistiveTouchCustomize#Reset
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#ActionsGroupSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#TapSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#DoubleTapSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/DoubleTapSpecifier#ASTDoubleTapTimeoutSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#LongPressSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/LongPressSpecifier#ASTLongPressDurationSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#CustomGestureHeading
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#CreateCustomGesture
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#IdleOpacity
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#MouseDevicesHeaderTitle
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#AssistiveTouchMouseDevices
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/AssistiveTouchMouseDevices#BluetoothDevicesScanning
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#AssistiveTouchMouseKeys
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization#MOUSE_POINTER_SIZE_TITLE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization#MOUSE_POINTER_VISUAL_APPEARANCE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization#MOUSE_POINTER_COLOR
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization/MOUSE_POINTER_COLOR#CustomizeMouseButtons
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization#MOUSE_POINTER_TIMEOUT
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE/ASTMousePointerCustomization/AMOUSE_POINTER_TIMEOUT#Auto-Hide
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#AlwaysShowSoftwareKeyboard
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#AlwaysShowMenu
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#DwellEnabledSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/AIR_TOUCH_TITLE#DwellToleranceSpecifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#ForceTouch
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#FORCE_TOUCH
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#ForceTouchAccessibilityMasterSwitch
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#FourceTouchSensitivityGroupIdentifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#timingGroup
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#HapticTouchFastIdentifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#HapticTouchSlowIdentifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/ForceTouch#FourceTouchSensitivityTestGroupIdentifier
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#TOUCH_ACCOMMODATIONS
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#TOUCH_ACCOMMODATIONS_SWITCHER
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#HoldDurationGroup
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#HoldDuration
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#IgnoreRepeatGroup
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#IgnoreRepeat
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#Tap%20Assistance
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#OFF
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#ACTIVATE_ON_TOUCH
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/TOUCH_ACCOMMODATIONS#ACTIVATE_ON_RELEASE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#TAP_TO_WAKE_TITLE
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#SHAKE_TO_UNDO
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#VIBRATION
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE#CALL_AUDIO_ROUTING
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/CALL_AUDIO_ROUTING#CALL_AUDIO_ROUTING_AUTOMATIC
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/CALL_AUDIO_ROUTING#CALL_AUDIO_ROUTING_HEADSET
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/CALL_AUDIO_ROUTING#CALL_AUDIO_ROUTING_SPEAKER
prefs:root=ACCESSIBILITY&path=TOUCH_REACHABILITY_TITLE/CALL_AUDIO_ROUTING#callAudioRoutingAutoAnswer

Settings ⇾ Accessibility ⇾ Face ID & Attention:
───────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=FACE_ID
prefs:root=ACCESSIBILITY&path=FACE_ID#PearlUnlockAttention
prefs:root=ACCESSIBILITY&path=FACE_ID#AttentionAware
prefs:root=ACCESSIBILITY&path=FACE_ID#PearlSuccessHapticGroup
prefs:root=ACCESSIBILITY&path=FACE_ID#PearlSuccessHaptic

Settings ⇾ Accessibility ⇾ Switch Control:
──────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#EnablingCell
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#SwitchesIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/SwitchesIdentifier#AddSwitchIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/SwitchesIdentifier#BluetoothDevicesIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#RecipesIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#ScanningStyleIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanningStyleIdentifier#AUTO_SCANNING_LABEL
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanningStyleIdentifier#MANUAL_SCANNING_LABEL
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanningStyleIdentifier#DWELL_SCANNING_LABEL
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#TimingIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#ScanningSpeedIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanningSpeedIdentifier#NumericalPreferencePickerGroupIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#DelayAfterInputIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/DelayAfterInputIdentifier#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#ActionRepeatIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ActionRepeatIdentifier#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#LongPressIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/LongPressIdentifier#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#TapBehaviorIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/TapBehaviorIdentifier#TapBehaviorDefault
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/TapBehaviorIdentifier#TapBehaviorAuto
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/TapBehaviorIdentifier#AlwaysTap
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#ScanLocationIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanLocationIdentifier#ScanAfterTapFirst
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/ScanLocationIdentifier#ScanAfterTapCurrent
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#SwitchKeyboardIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#RestartScanAtCurrentIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#AlwaysTapKeyboardIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#UseExtendedKeyboardPredictionsIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#SwitchStabilityIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#HoldDurationIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/HoldDurationIdentifier#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#IgnoreRepeatIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/IgnoreRepeatIdentifier#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#AxisSelectionGroupIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#AxisSweepIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/AxisSweepIdentifier#SelectionStyleGroup
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/AxisSweepIdentifier#SelectionStyleSingle
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/AxisSweepIdentifier#SelectionStyleRefined
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/AxisSweepIdentifier#SelectionStylePrecise
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/AxisSweepIdentifier#AxisSweepSpeed
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#CameraPointPickerSwitch
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/CameraPointPickerSwitch#CameraPointPickerSwitcher
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#AudioGroupIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#SoundIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#SpeechIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/SpeechIdentifier#VoicesIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/SpeechIdentifier#SpeechRateIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#CustomizeMenuIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#ItemGroupingIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#VisualGroupIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#CursorVisibilityIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle#CustomGesturesIdentifier
prefs:root=ACCESSIBILITY&path=ScannerSwitchTitle/CustomGesturesIdentifier#CreateCustomGesture

Settings ⇾ Accessibility ⇾ Voice Control:
─────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#SETUP_COMMAND_AND_CONTROL
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#COMMAND_AND_CONTROL_LANGUAGE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle/COMMAND_AND_CONTROL_LANGUAGE#English%20(United%20States)
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#CUSTOMIZE_COMMANDS
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#VOCABULARY
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#UPON_COMMAND_RECOGNITION_TITLE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#SHOW_TEXT_RESPONSE_TITLE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#PLAY_SOUND_RESPONSE_TITLE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#USER_HINTS_SHOW_HINTS_TITLE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#ALWAYS_SHOW_OVERLAY_GROUP_TITLE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#ALWAYS_SHOW_OVERLAY
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle/ALWAYS_SHOW_OVERLAY#OVERLAY_NONE
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle/ALWAYS_SHOW_OVERLAY#OVERLAY_NUMBERS
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle/ALWAYS_SHOW_OVERLAY#OVERLAY_NAMES
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle/ALWAYS_SHOW_OVERLAY#OVERLAY_GRID
prefs:root=ACCESSIBILITY&path=CommandAndControlTitle#ATTENTION_AWARE_ACTION

Settings ⇾ Accessibility ⇾ Side Button (or Home Button):
────────────────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HOME_SPEED_HEADER
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HOME_CLICK_SPEED_DEFAULT
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HOME_CLICK_SPEED_SLOW
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HOME_CLICK_SPEED_SLOWEST
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HomeButtonAssistantTitle
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HomeButtonAssistantSiri
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HomeButtonAssistantVoiceControl
prefs:root=ACCESSIBILITY&path=HOME_CLICK_TITLE#HomeButtonAssistantOff

Settings ⇾ Accessibility ⇾ Apple TV Remote:
───────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=APPLE_TV_REMOTE
prefs:root=ACCESSIBILITY&path=APPLE_TV_REMOTE#AppleTVSimpleGestures

Settings ⇾ Accessibility ⇾ Keyboards:
─────────────────────────────────────
prefs:root=ACCESSIBILITY&path=KEYBOARDS
prefs:root=ACCESSIBILITY&path=KEYBOARDS#FULL_KEYBOARD_ACCESS
prefs:root=ACCESSIBILITY&path=KEYBOARDS/FULL_KEYBOARD_ACCESS#FKAEnabledSwitch
prefs:root=ACCESSIBILITY&path=KEYBOARDS/FULL_KEYBOARD_ACCESS#APPEARANCE
prefs:root=ACCESSIBILITY&path=KEYBOARDS/FULL_KEYBOARD_ACCESS#FKAFocusRingTimeout
prefs:root=ACCESSIBILITY&path=KEYBOARDS/FULL_KEYBOARD_ACCESS#FKAFocusRingHighVisibilityEnabled
prefs:root=ACCESSIBILITY&path=KEYBOARDS/FULL_KEYBOARD_ACCESS#FKAFocusRingColor
prefs:root=ACCESSIBILITY&path=KEYBOARDS#KEY_REPEAT
prefs:root=ACCESSIBILITY&path=KEYBOARDS/KEY_REPEAT#KeyRepeatEnabled
prefs:root=ACCESSIBILITY&path=KEYBOARDS/KEY_REPEAT#KeyRepeatInterval
prefs:root=ACCESSIBILITY&path=KEYBOARDS/KEY_REPEAT#KeyRepeatDelay
prefs:root=ACCESSIBILITY&path=KEYBOARDS#STICKY_KEYS
prefs:root=ACCESSIBILITY&path=KEYBOARDS/STICKY_KEYS#StickyKeysEnabled
prefs:root=ACCESSIBILITY&path=KEYBOARDS/STICKY_KEYS#StickyKeysShiftToggle
prefs:root=ACCESSIBILITY&path=KEYBOARDS/STICKY_KEYS#StickyKeysSound
prefs:root=ACCESSIBILITY&path=KEYBOARDS#SLOW_KEYS
prefs:root=ACCESSIBILITY&path=KEYBOARDS/SLOW_KEYS#NumericalPreferenceSwitcherIdentifier
prefs:root=ACCESSIBILITY&path=KEYBOARDS#SOFTWARE_KEYBOARDS
prefs:root=ACCESSIBILITY&path=KEYBOARDS#LOWERCASE_KEYBOARD

Settings ⇾ Accessibility ⇾ Hearing Devices:
───────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=HEARING_AID_TITLE
prefs:root=ACCESSIBILITY&path=HEARING_AID_TITLE#AvailableAidsHeading
prefs:root=ACCESSIBILITY&path=HEARING_AID_TITLE#HEARING_AID_BLUETOOTH
prefs:root=ACCESSIBILITY&path=HEARING_AID_TITLE#HEARING_AID_COMPLIANCE

Settings ⇾ Accessibility ⇾ Sound Recognition:
─────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=SOUND_RECOGNITION_TITLE
prefs:root=ACCESSIBILITY&path=SOUND_RECOGNITION_TITLE#Sounds

Settings ⇾ Accessibility ⇾ RTT/TTY:
───────────────────────────────────
prefs:root=ACCESSIBILITY&path=RTT
prefs:root=ACCESSIBILITY&path=RTT#SW_TTY
prefs:root=ACCESSIBILITY&path=RTT#HW_TTY

Settings ⇾ Accessibility ⇾ Audio/Visual:
────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#AXPAAudioGroupSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#AXPAEnableSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE/AXPAEnableSpecID#AXPAEnableSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE/AXPAEnableSpecID#AXPAPersonalAudioSetupSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#AXPAMonoSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#AXPANoiseSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#AXPABalanceSpecID
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#VISUAL_HEADING
prefs:root=ACCESSIBILITY&path=AUDIO_VISUAL_TITLE#LED_FLASH

Settings ⇾ Accessibility ⇾ Subtitles & Captioning:
──────────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=SUBTITLES_CAPTIONING
prefs:root=ACCESSIBILITY&path=SUBTITLES_CAPTIONING#currentTheme

Settings ⇾ Accessibility ⇾ Guided Access:
─────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE#EnableGuidedAccess
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE#GuidedAccessSecurityLinkList
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE/GuidedAccessSecurityLinkList#GAXPinButton
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE#GuidedAccessTimeRestrictionsLinkList
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE/GuidedAccessTimeRestrictionsLinkList#GUIDED_ACCESS_TIME_RESTRICTIONS_HEADING
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE/GuidedAccessTimeRestrictionsLinkList#GUIDED_ACCESS_TIME_RESTRICTIONS_SOUND_TITLE
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE/GuidedAccessTimeRestrictionsLinkList#GUIDED_ACCESS_TIME_RESTRICTIONS_SPEAK_TITLE
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE#GuidedAccessEnableAXFeatures
prefs:root=ACCESSIBILITY&path=GUIDED_ACCESS_TITLE#GuidedAccessAutoLockTime

Settings ⇾ Accessibility ⇾ Siri:
────────────────────────────────
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#SIRI_SETTINGS_TYPE_TO_SIRI
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#VOICE_FEEDBACK_GROUP_ID
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#VOICE_FEEDBACK_ALWAYS_ID
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#VOICE_FEEDBACK_WITH_SWITCH_ID
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#VOICE_FEEDBACK_HANDSFREE_ID
prefs:root=ACCESSIBILITY&path=SIRI_SETTINGS_TITLE#SIRI_SETTINGS_VOICE_ACTIVATION_ALWAYS_ALLOW

Settings ⇾ Accessibility ⇾ Accessibility Shortcut:
──────────────────────────────────────────────────
prefs:root=ACCESSIBILITY&path=TRIPLE_CLICK_TITLE
	•	Shortcuts:
Open = shortcuts://

Create new shortcut = shortcuts://create-shortcut

Install shortcut = shortcuts://shortcuts/ShortcutID

Open gallery = shortcuts://gallery

Open shortcut = shortcuts://open-shortcut?name=Your%20Shortcuts%20Name

Run shortcut = shortcuts://run-shortcut?name=Your%20Shortcuts%20Name

Run shortcut with text string input = shortcuts://run-shortcut?name=Your%20Shortcuts%20Name&input=text&text=What%20You%20Want%20To%20Input

Run shortcut with input from clipboard = shortcuts://run-shortcut?name=Your%20Shortcuts%20Name&input=clipboard
	•	Stocks:
Open = stocks://
	•	Tips:
Open = x-tips-widget://  (unverified)
	•	TV:
Open = videos://
	•	Voice Memos:
Open = voicememos://  (could work in the Notification Center)
	•	Wallet:
Open = shoebox://
	•	Watch:
Open = itms-watch://
       itms-watchs://
	•	Workflow:
Open = workflow://

Create workflow = workflow://create-workflow

Open a workflow = workflow://open-workflow?name=TheNameOfWorkflow

Run a workflow = workflow://run-workflow?name=TheNameOfWorkflow&input=Input

Open the gallery = workflow://gallery

Search the gallery = workflow://gallery/search?query=YourQuery

Install workflow = workflow://shortcuts/ShortcutID  (unverified)
                   workflow://workflows/WorkflowID  (unverified)
Third-Party Apps & Services
Just like the list above, the below apps will mostly show the basic open links for third-party apps, and some of the URIs may also come attached with more detailed deep links.
	•	360 Web Browser:
Open = 360://
	•	6pm:
Open = sixpm://
	•	8mm Vintage Camera:
Open = nx8mm://
	•	Achievement - Reward Health:
Open = achievement://
	•	Age of Solitaire : Build City:
Open = fb1431194636974533://
	•	Agenda.:
Open = agenda://
       agenda-notes://
	•	Airbnb:
Open = airbnb://
	•	AirDroid - File Transfer&Share:
Open = sandstudio-airdroid://
	•	Airmail:
Open = airmail://

Start draft = airmail://compose

Start draft with recipient = airmail://compose?to=TheirEmailAddress

Start draft with recipient, cc = airmail://compose?to=TheirEmailAddress&cc=TheirEmailAddress

Start draft with recipient, bcc = airmail://compose?to=TheirEmailAddress&bcc=TheirEmailAddress

Start draft with recipient, subject = airmail://compose?to=TheirEmailAddress&subject=YourSubjectText

Start draft with recipient, body = airmail://compose?to=TheirEmailAddress&plainBody=YourBodyText

Start draft with recipient, HTML body = airmail://compose?to=TheirEmailAddress&htmlBody=YourBodyHTML

Start draft with recipient, CC, BCC, subject, body = airmail://compose?to=TheirEmailAddress&cc=TheirEmailAddress&bcc=TheirEmailAddress&subject=YourSubjectText&plainBody=YourBodyText

[You can make other combinations above using the above identifiers]
	•	Airtable:
Open = airtable://
	•	Alpha Omega:
Open = fb1414385748867269suffix://
	•	Amazon Alexa:
Open = alexa://
	•	Amazon Fire TV:
Open = firetv://
	•	AMC Theatres:
Open = amc://
	•	Amperes Lite battery charging:
NONE
	•	AmpliFi WiFi:
Open = fb1761190244145574amplifi://
	•	Amwell: Doctor Visits 24/7:
Open = amwell://
	•	Ancestry:
Open = ancestry://
	•	Anchor:
Open = anchorfm://
       anchorfmspotify://
	•	Any.do: To do list & Calendar:
Open = anydo://
       any.do://
       anydoNewVersion://
       com.anydo.AnyDO
       en-anydo://
	•	Asana: organize tasks & work:
Open = asana://
	•	Autodesk SketchBook:
Open = sketchbook://
	•	Baidu Netdisk - Free up mobile phone space:
Open = baidunetdisk://
       baidunetdiskshareinvite://
       baiduWallet20140625://
       baiduyun://
       baiduyunhb://
       baiduyunmbox://
       bdnetdisk://
       bdnetdiskapp://
       bdnetdiskwap://
       tencent101455621://
       tencent101524405://
	•	Ballz:
Open = com.ketchapp.ballz://
	•	Bank of America Mobile Banking:
Open = bofa://
	•	Battery Life - check runtimes:
Open = Battery-Life://
	•	Best Buy:
Open = bestbuy://
	•	Bejeweled Blitz:
Open = com.popcap.ios.BejBlitz://
       com.popcap.ios.BejBlitz.From.Bej3://
       com.popcap.ios.BejBlitz.From.Bej2://
       ea850758://
       ea47862://
	•	Bitmoji:
Open = placeholder://
       imoji://
       bitmoji-sdk://
	•	Blockchain Wallet: Buy Bitcoin:
Open = blockchain://
       blockchain-wallet://
       bitcoin://  (may also open other wallets like Coinbase Wallet)
	•	Bonza Word Puzzle:
Open = bonzapuzzles://
	•	Brave Private Browser & VPN:
Open = brave://

Open URL = brave://open-url?url=
	•	Brushstroke:
Open = brushstroke://
	•	Buddhify: meditation on the go:
Open = com.21awake.buddhify2://
	•	BURGER KING® App
Open = burgerking://
	•	Cake Browser:
Open = cakeslice://
       havecake://
	•	Camera+:
Open = cameraplus://
	•	Canva: Graphic Design & Video:
Open = canvaeditor://
	•	Carb Manager: Keto Diet App:
Open = carbmanager://
	•	Cash App:
Open = squarecash://
       cashme://
       •	Chase Mobile Banking
Open = ydl://
	•	Citi Mobile:
Open = citiglobal://
	•	Clash of Clans:
Open = clashofclans://
       wxfa242abf8cdd841a://
       tencent1105771533://
       tencentlaunch1105771533://
	•	Coinbase - Buy & sell Bitcoin:
Open = com.coinbase.accounts://
       com.coinbase.consumer://
       com.coinbase.dashboard://
       com.coinbase.identity-verification://
       com.coinbase.oauth://
       com.coinbase.oauth.app-to-app://
       com.coinbase.oauth-authorize://
       com.coinbase.oauth.universal-links://
       com.coinbase.release://

       basic-attention-token://
       bitcoin://  (may also open wallets like Coinbase Wallet and Blockchain Wallet)
       bitcoin-cash://
       ethereum://  (may also open wallets like Coinbase Wallet)
       litecoin://  (may also open wallets like Coinbase Wallet)
       usdc://
       zcash://
	•	Coinbase Wallet:
Open = bitcoin://  (may also open other wallets like Blockchain Wallet)
       ethereum://  (may also open other apps like Coinbase)
       litecoin://  (may also open other apps like Coinbase)
	•	CPlus for Craigslist:
Open = fb444280555728352://
	•	Dashlane - Password Manager:
Open = dashlane://
       dashlane-ext://
       org-appextension-feature-password-management://  (may open other password managers such as 1Password, Keeper, or LastPass)
	•	Deezer: Music & Podcast Player:
Open = deezer://
       deezer-query://
       com.deezer.Deezer://
       wazedeezer://

Open album = deezer-query://www.deezer.com/artist?query=ALBUM%20NAME

Open artist = deezer-query://www.deezer.com/artist?query=ARTIST%20NAME

Open playlist = deezer-query://www.deezer.com/playlist?query=PLAYLIST%20NAME

Open search = deezer://www.deezer.com/search

Open a specific search page = deezer://www.deezer.com/search/SEARCH%20TERM
	•	DICK'S Sporting Goods, Fitness:
Open = app://
	•	Diptic:
NONE
	•	DocuSign - Upload & Sign Docs:
Open = docusignit://
       docusign-v1://
       appx://
	•	Dolphin Browser:
Open = dolphin://
	•	DoorDash - Food Delivery:
Open = doordash://
       com.doordash.consumer.dev.braintree://
       doordash.DoorDashConsumer.braintree://
	•	DoubleTake by FiLMiC Pro:
Open = doubletake://
	•	Drafts:
Open = drafts://

Create new draft = drafts://create?
                   drafts://x-callback-url/create?

Create new draft with text = drafts://create?text=The%20Text%20You%20Want%20To%20Write
                             drafts://x-callback-url/create?text=The%20Text%20You%20Want%20To%20Write

Create new draft with text and tweet it = drafts://create?text=The%20Text%20You%20Want%20To%20Write&action=Tweet%3A%20YourTwitterUsername
                                          drafts://x-callback-url/create?text=The%20Text%20You%20Want%20To%20Write&action=Tweet%3A%20YourTwitterUsername

Create new draft with text, tweet it, and return to Drafts = drafts://x-callback-url/create?text=The%20Text%20You%20Want%20To%20Write&action=Tweet%3A%20YourTwitterUsername&x-success=drafts%3A//

* See 'Fantastical' app below for an example of a URL scheme
  you can run from within Drafts.

* See MacStories' article on using Drafts to create custom
  actions with URL schemes and custom Drafts tags like
  [[draft]], [[title]], [[clipboard]], and [[line|..n]].
  It's an older article but very much applicable today, and
  it goes over custom Drafts URL schemes in detail.
  https://www.macstories.net/tutorials/guide-url-scheme-ios-drafts
	•	Draw Something:
Open = fb225826214141508paid://
	•	DropBox:
Open = db-auth://
       db-wopi://
       db-wopi-callback://
       dbx-dropbox://
       dbx-dropbox-supporting-emm-1://
       dbapi-1://
       dbapi-2://
       dbapi-3://
       dbapi-4://
       dbapi-5://
       dbapi-6://
       dbapi-7://
       dbapi-8://
       dbapi-9://
       dbapi-10://
	•	DuckDuckGo Privacy Browser:
Open = ddgLaunch://  (older versions of the app only)
       ddgQuickLink://
       ddgFavorite://
       http://  (defaults to Safari if Safari is installed)
       https://  (defaults to Safari if Safari is installed)

Open new search = ddgNewSearch://
                  ddgFire://

Open search results = ddgQuickLink://the%20search%20term
                      ddgFavorite://the%20search%20term

Open website = ddgQuickLink://thewebsiteurl
               ddgFavorite://thewebsiteurl
               http://thewebsiteurl  (defaults to Safari if Safari is installed)
               https://thewebsiteurl  (defaults to Safari if Safari is installed)

Open bookmarks = ddgBookmarks://

Open favoriting instructions = ddgAddFavorite://

* Bangs do not work in URL schemes from Shortcuts.
  At least, I haven't gotten them to work. They do
  work in URL schemes of other browsers, like Safari,
  Chrome, and Firefox, but not all. You can view all
  bangs at https://duckduckgo.com/bang.

  Bang examples for Null Byte's site:
  Safari: https://duckduckgo.com/?q=!nullbyte+kali+linux
  Chrome: googlechrome://duckduckgo.com/?q=!nullbyte+kali+linux
  Firefox: firefox://open-url?url=https://duckduckgo.com/?q=!nullbyte+kali+linux

* URL parameters also do not work in URL schemes
  from Shortcuts. Again, I haven't been able to
  get them working. They do work in URL schemes
  of other browsers, like Safari and Chrome, but
  not all (Firefox is troublesome). You can view
  all parameters at https://duckduckgo.com/params.
	•	Duolingo:
Open = duolingo://
       com.duolingo.DuolingoMobile://
	•	Enlight Videoleap Video Editor:
Open = videoleap://
	•	ESPN: Live Sports & Scores:
Open = sportscenter://
       sportscenterdl://
       com.espn.ScoreCenter://
       sportscenter421://
       gsd-sportscenter://
	•	Evernote:
Open = Evernote://
	•	Facebook:
Open = fb://
	•	Facebook Business Suite:
Open = fb-biz://
       fb-pma-diode://
       fb-pma://
	•	Facetune:
Open = facetune://
	•	Facetune2 by Lightricks:
Open = facetune2://
	•	Fandango:
Open = fandango://
	•	Fantastical - Calendar & Tasks:
Open = fantastical://
       fantastical2://

Create new event = fantastical://x-callback-url/parse
                   fantastical2://x-callback-url/parse

Create new named event = fantastical://x-callback-url/parse?sentence=Your%20Event%20Name
                         fantastical2://x-callback-url/parse?sentence=Your%20Event%20Name

When run from Drafts app as a new action (premium Drafts subscription required)
───────────────────────────────────────────────────────────────────────────────
Create new event from current draft = fantastical2://x-callback-url/parse?sentence=[[draft]]

Create new event from current draft then return to Drafts = fantastical2://x-callback-url/parse?sentence=[[draft]]&x-success=drafts%3A//
	•	FiLMiC Pro — Video Camera:
Open = filmicpro://
	•	Firefox: Private, Safe Browser:
Open = firefox://

Open URL = firefox://open-url?url=
	•	Firefox Focus: Privacy browser:
Open = firefox-focus://

Open URL = firefox-focus://open-url?url=
	•	Fitbit:
Open = fitbit://
	•	Flickr:
Open = flickr://
	•	FOX NOW: Watch TV & Sports:
Open = foxapp://
	•	Game of Thrones Beyond the Wall:
Open = fb300802074142783://
	•	Gboard:
Open = gboard://
	•	Gmail - Email by Google:
Open = googlegmail://
	•	Goodreads: Book Reviews:
Open = goodreads://
	•	Google:
Open = google://
	•	Google Assistant:
Open = googleassistant://
       comgoogleopa://
       comgoogleopaulr://
	•	Google Calendar:
Open = googlecalendar://
	•	Google Docs:
Open = googledocs://
       googledocs-v2://
       com.google.sso.263492796725://
	•	Google Chrome:
Open = googlechrome://

Open website = googlechrome://thewebsiteurl
	•	Google Drive:
Open = googledrive://
	•	Google Earth:
Open = googleearth://
       comgoogleearth://
	•	Google Home:
Open = googlehome://
       chromecast://
       chromecast-la://
	•	Google Keep:
Open = comgooglekeep://
	•	Google Maps - GPS Navigation:
Open = googlemaps://
	•	Google Photos:
Open = googlephotos://
	•	Google Sheets:
Open = googlesheets://
	•	Google Translate:
Open = googletranslate://
	•	Google Voice:
Open = googlevoice://
	•	Gospel Library:
Open = gospellibrary://
	•	Halide Camera:
Open = halide://
	•	Headspace: Meditation & Sleep:
Open = headspace://
	•	HEOS:
Open = heosbydenon://
	•	HBO GO:
Open = hbogo://  (unverified)
	•	HBO NOW:
Open = hbonow://
	•	Hulu: Watch TV Shows & Movies:
Open = hulu://
	•	Hyperlapse from Instagram:
Open = hyperlapse://
	•	iCab Mobile (Web Browser):
Open = x-icabmobile://
	•	IMDb Movies & TV:
Open = imdb://
	•	Insight Timer - Meditation App:
Open = insight://
	•	Instagram:
Open = instagram://
	•	Kahoot! Play & Create Quizzes:
Open = kahoot://
	•	Kasa Smart:
Open = kasa://
	•	Keeper Password Manager:
Open = keeper://
       keepersecurity://
       org-appextension-feature-password-management://  (may open other password managers such as 1Password, Dashlane, or LastPass)
	•	LastPass Password Manager:
Open = lastpass://
       com.lastpass.ilastpass.iacdistribution://
       com.lastpass.ilastpass://
       lastpass-launch://
       lastpass-multifactor://
       org-appextension-feature-password-management://  (may open other password managers such as 1Password, Dashlane, or Keeper)
	•	Launch Center Pro:
Open = launch://  (unverified)
	•	Launcher with Multiple Widgets:
Open = launcher://
	•	Learn Languages with Memrise:
Open = memrise://
	•	Litely:
Open = litely://
	•	Lose It! – Calorie Counter:
Open = loseit://
	•	Mercury Web Browser Pro - with powerful Ad Block extension:
Open = merc://
	•	Messenger:
Open = fb-messenger://

Share page = fb-messenger-share://
	•	Microsoft Authenticator:
Open = msauth://
	•	Microsoft Edge:
Open = microsoft-edge://

Open URL = microsoft-edge-http://URL
           microsoft-edge-https://URL
           http-intunemam://URL
           https-intunemam://URL

Others:
───────
x-msauth-microsoft-edge-https://
x-msauth-microsoft-edge-https-intunemam://
microsoft-edge-http-intunemam://
microsoft-edge-https-intunemam://
microsoft-edge-intunemam://
	•	Microsoft Outlook:
Open = ms-outlook://
       ms-outlook-shared://
       com.microsoft.Office.Outlook://
       ms-outlook-accepts-attachments://
       x-msauth-outlook-prod://

Open for Intune mobile app management = ms-outlook-intunemam://
                                        ms-outlook-accepts-attachments-intunemam://
	•	Microsoft Planner:
Open = planner://
	•	Microsoft PowerPoint:
Open = powerpoint://
	•	Microsoft SharePoint:
Open = ms-sharepoint://
	•	Microsoft Teams:
Open = msteams://
	•	Microsoft Word:
Open = word://
	•	MoviePass:
Open = moviepass://
	•	MSNBC:
Open = msnbctve://
	•	Netflix:
Open = nflx://
	•	NordVPN: VPN Fast & Secure:
Open = nordvpn://
	•	Opera Mini:
Open = opera-://
	•	PayPal: Mobile Cash:
Open = paypal://
	•	Peloton — at home fitness:
Open = pelotoncycle://
	•	Photon Flash Player for iPhone - Flash Video & Games plus Private Web Browser:
Open = photon://
	•	PhotoScan by Google Photos:
Open = photoscan://
	•	PicsArt Photo & Video Editor:
Open = picsart://
	•	Pinterest:
Open = pinterest://
	•	PlayStation App:
Open = scepsapp://
	•	Pocket: Save. Read. Grow.:
Open = pocket://
       readitlater://
       pocket-oauth-v1://
       en-readitlater-5776://
       com.ideashower.ReadItLaterPro3://
       com.ideashower.ReadItLaterPro://
       com.ideashower.ReadItLaterProAlpha://
       com.ideashower.ReadItLaterProEnterprise://
	•	Polymail:
Open = polymail://
	•	ProtonMail - Encrypted Email:
Open = protonmail://
	•	Puffin Browser:
Open = puffin://
	•	Quizizz: Play to Learn:
Open = quizizz://
	•	QQ Browser HD:
Open = mttbrowserhd://  (unverified)

Open URL = mttbrowserhd://url=  (unverified)
	•	Reddit:
Open = reddit://
	•	Reflectly:
Open = reflectly://
       reflectlylink://
	•	Rosetta Stone: Learn Languages:
Open = rstotalecompanion://
       learnlanguages://
	•	Sam's Club:
Open = samsiphone://
       samsclub://
	•	SAP Concur:
Open = concurmobile://
       concurmobiledeeplink://
	•	SAP Concur Events 2020:
Open = concur://
	•	Shazam:
Open = shazam://
       shazam-v8://
       com.shazam.Shazam://
       com.shazam.encore.Shazam://
       shazamfree://
	•	Seesaw Class:
Open = seesaw://
	•	ServiceNow Agent:
Open = snappauth://
       snagent://
	•	ServiceNow Agent - Intune:
Open = snappauth://
       snagent://
       snappauth-intunemam://
       snagent-intunemam://
	•	ServiceNow Mobile:
Open = snempappauth://
       snrequest://
	•	ServiceNow Mobile - Intune:
Open = snempappauth://
       snrequest://
       snempappauth-intunemam://
       snrequest-intunemam://
	•	ServiceNow Support:
Open = snsupportappauth://
       snsupport://
	•	Signal - Private Messenger:
Open = sgnl://
	•	SimpleMind+ Mind Mapping:
Open = simplemind://
	•	Skype for iPhone:
Open = skype://
	•	Slack:
Open = slack://
	•	Sleep Cycle: smart alarm clock:
Open = sleepcycle://
	•	Snapchat:
Open = snapchat://
	•	SoundHound - Music Discovery:
Open = soundhound://
	•	Spark:
Open = readdle-spark://

Start draft = readdle-spark://compose

Identifiers to tack onto the start draft scheme:
[add "?" after "compose" for first one]
[then add "&" for each additional one]
────────────────────────────────────────────────
Add recipient address = recipient=TheirEmailAddress
Add email subject = subject=YourSubjectText
Add email body text = body=YourBodyText
Add cc recipient address = cc=TheirEmailAddress
Add bcc recipient address = bcc=TheirEmailAddress

Examples of identifier combinations:
────────────────────────────────────
Start draft with recipient = readdle-spark://compose?recipient=TheirEmailAddress

Start draft with recipient, subject = readdle-spark://compose?recipient=TheirEmailAddress&subject=YourSubjectText

Start draft with recipient, subject, body = readdle-spark://compose?recipient=TheirEmailAddress&subject=YourSubjectText&body=YourBodyText

Start draft with recipient, cc, bbc, subject, body = readdle-spark://compose?recipient=TheirEmailAddress&cc=TheirEmailAddress&bcc=TheirEmailAddress&subject=YourSubjectText&body=YourBodyText
	•	Speedtest by Ookla:
Open = speedtest://
	•	Spotify Music:
Open = spotify://
	•	Steam Chat:
Open = steamchatmobile://
	•	Steller:
Open = steller://
	•	Streaks:
Open = streaks://
	•	Synology Drive:
Open = synodrive://
	•	TeamViewer: Remote Control:
Open = tvcontrol1://
	•	Telegram Messenger:
Open = telegram://
       tg://
       tgapp://
       ton://
	•	Today Habit tracker:
Open = today://
       todayCheckinHabit://
	•	Trello:
Open = trello://
	•	Tripadvisor Hotels & Vacation:
Open = tripadvisor://
	•	Tumblr:
Open = tumblr://  (unverified)
	•	TuneIn Radio: Live News, Music:
Open = tunein://
	•	Twitch:
Open = twitch://
	•	Twitter:
Open = twitter://
	•	TweetBot for Twitter:
Open = tweetbot://  (unverified)
	•	Uber - Request a ride:
Open = uber://
	•	UC Browser:
Open = ucbrowser://
	•	Udemy Online Video Courses:
Open = udemy://
	•	UpKeep Work Order Maintenance:
Open = com.upkeep://
	•	VelocityEHS:
Open = com.velocityehs.velocityehs://
	•	Vimeo:
Open = vimeo://  (unverified)
	•	VSCO:
Open = vsco://
	•	Waze Navigation & Live Traffic:
Open = waze://
	•	Weather Underground: Local Map:
Open = wxunderground://
	•	WGT Golf:
Open = worldofgolf://
       wgtapp://
	•	WhatsApp Messenger:
Open = whatsapp://
	•	The White House:
None
	•	WiFi Map: Find Internet & VPN:
Open = freewifimap://
	•	Words with Friends Classic:
Open = WordsWithFriends3://
       amzn-com.zynga.WordsWithFriends3://
	•	Words with Friends 2 Word Game:
Open = WordsWithFriends3://
       amzn-com.zynga.WordsWithFriends3://
	•	Workday:
Open = workday+https://     (opens but with a missing web address error)

Open and configure = workday+https://wd5.myworkday.com.TenantName
	•	Workday Countdown:
Open = workdaycountdown://
	•	Wunderlist: To-Do List & Tasks:
Open = wunderlist://
	•	Yandex Browser:
Open URL = yandexbrowser-open-url://
	•	YNAB (You Need A Budget):
Open = ynab://
	•	YouTube: Watch, Listen, Stream:
Open = youtube://
	•	Zelle:
Open = zelle://
       com.zellepay.zelle://
	•	ZOOM Cloud Meetings:
Open = zoomus://
	•	ZuluDesk Student:
Open = zuludesk://
If you know the URL scheme name or action to an app not featured here, let us know. We encourage the support of our community to help us build this list up!
Also, it's worth noting that Apple has been trying to wean developers off URL schemes since iOS 9.2 in favor of universal links, but URL schemes are nowhere near dead. And with Apple turning Workflow into its own Shortcuts app starting in iOS 12, an app that even has its own scheme, there's no reason to believe URL schemes are going away anytime soon.
Cover image by Jake Peterson/Gadget Hacks; Screenshots by Justin Meyers/Gadget Hacks 
