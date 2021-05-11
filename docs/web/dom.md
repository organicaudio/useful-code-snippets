# dom vs. virtual dom vs. shadow dom

## dom (browser)

The html document object model (dom) is an API that allows the manipulation of a webpage by representing the structure of a html document.

[Source](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

## virtual dom (framework)

A virtual dom is designed to optimize calls to the real dom. A change in the dom leads to a rendering of the webpage, which is in comparison a slow operation. So javascript frameworks (like react.js) keep a copy of the dom (the virtual dom) which allows them to bundle changes before updating the dom.

[Source](https://reactjs.org/docs/faq-internals.html)

## shadow dom (browser)

A shadow dom allows the encapsulation of structure, style and behavior inside another dom. A shadow dom is a hidden separated dom which can be attached to an html element.

[Source](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)