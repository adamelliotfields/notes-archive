# JavaScript Web API Reference

## [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
The Document Object Model (DOM) is a programming interface for HTML, XML and SVG documents. It provides a structured representation of the document as a tree. The DOM defines methods that allow access to the tree, so that they can change the document structure, style and content. The DOM provides a representation of the document as a structured group of nodes and objects, possessing various properties and methods. Nodes can also have event handlers attached to them, and once an event is triggered, the event handlers get executed. Essentially, it connects web pages to scripts or programming languages.

Although the DOM is often accessed using JavaScript, it is not a part of the JavaScript language. It can also be accessed by other languages.

### [DOM Events](https://developer.mozilla.org/en-US/docs/Web/Events)
DOM Events are sent to notify code of interesting things that have taken place. Each event is represented by an object which is based on the Event interface, and may have additional custom fields and/or functions used to get additional information about what happened. Events can represent everything from basic user interactions to automated notifications of things happening in the rendering model.

[DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)
 - The `DOMContentLoaded` event is fired when the initial HTML document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading.

[load](https://developer.mozilla.org/en-US/docs/Web/Events/load)
 - The `load` event is fired when a resource and its dependent resources have finished loading.

[click](https://developer.mozilla.org/en-US/docs/Web/Events/click)
 - The `click` event is fired when a pointing device button (usually a mouse's primary button) is pressed and released on a single element.

[keypress](https://developer.mozilla.org/en-US/docs/Web/Events/keypress)
 - The `keypress` event is fired when a key is pressed down and that key normally produces a character value.

[mouseover](https://developer.mozilla.org/en-US/docs/Web/Events/mouseover)
 - The `mouseover` event is fired when a pointing device is moved onto the element that has the listener attached or onto one of its children.

[mouseout](https://developer.mozilla.org/en-US/docs/Web/Events/mouseout)
 - The `mouseout` event is fired when a pointing device (usually a mouse) is moved off the element that has the listener attached or off one of its children.
 - Note that it is also triggered on the parent when you move onto a child element, since you move out of the visible space of the parent. 

[change](https://developer.mozilla.org/en-US/docs/Web/Events/change)
 - The change event is fired for `input`, `select`, and `textarea` elements when a change to the element's value is committed by the user. Unlike the `input` event, the `change` event is not necessarily fired for each change to an element's value.

[submit](https://developer.mozilla.org/en-US/docs/Web/Events/submit)
 - The `submit` event is fired when a form is submitted.
 - Note that `submit` is fired only on the form element, not the button or submit input. (Forms are submitted, not buttons.)

## [Window](https://developer.mozilla.org/en-US/docs/Web/API/window)
The `Window` object represents a window containing a DOM document; the `document` property points to the DOM document loaded in that window. A window for a given document can be obtained using the `document.defaultView` property.

### Window Properties
[Window.localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
 - The `localStorage` property allows you to access a local `Storage` object. `localStorage` is similar to `sessionStorage`. The only difference is that, while data stored in `localStorage` has no expiration time, data stored in `sessionStorage` gets cleared when the browsing session ends—that is, when the browser is closed.
 - It should be noted that data stored in either `sessionStorage` or `localStorage` is specific to the protocol of the page.

[Window.sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage)
 - The `sessionStorage` property allows you to access a session `Storage` object for the current origin. `sessionStorage` is similar to `localStorage`, the only difference is while data stored in `localStorage` has no expiration set, data stored in `sessionStorage` gets cleared when the page session ends. A page session lasts for as long as the browser is open and survives over page reloads and restores. Opening a page in a new tab or window will cause a new session to be initiated, which differs from how session cookies work.

## [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)
A `Node` is an interface from which a number of DOM types inherit, and allows these various types to be treated (or tested) similarly.

The following interfaces all inherit from Node its methods and properties: `Document`, `Element`, `CharacterData` (which `Text`, `Comment`, and `CDATASection` inherit), `ProcessingInstruction`, `DocumentFragment`, `DocumentType`, `Notation`, `Entity`, `EntityReference`.

These interfaces may return null in particular cases where the methods and properties are not relevant. They may throw an exception - for example when adding children to a node type for which no children can exist.

### Node Properties
[Node.innerText](https://developer.mozilla.org/en-US/docs/Web/API/Node/innerText)
 - `Node.innerText` is a property that represents the "rendered" text content of a node and its descendants. As a getter, it approximates the text the user would get if they highlighted the contents of the element with the cursor and then copied to the clipboard. 

[Node.textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
 - The `Node.textContent` property represents the text content of a node and its descendants.

### Node Methods
[Node.removeChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
 - The `Node.removeChild()` method removes a child node from the DOM and returns the removed node.

[Node.appendChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
 - The `Node.appendChild()` method adds a node to the end of the list of children of a specified parent node. If the given child is a reference to an existing node in the document, `appendChild()` moves it from its current position to the new position (there is no requirement to remove the node from its parent node before appending it to some other node).

[Node.cloneNode()](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode)
 - The `Node.cloneNode()` method returns a duplicate of the node on which this method was called.

## [ParentNode](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)
The `ParentNode` interface contains methods that are particular to `Node` objects that can have children.

`ParentNode` is a raw interface and no object of this type can be created; it is implemented by `Element`, `Document`, and `DocumentFragment` objects.

### ParentNode Properties
[ParentNode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)
 - `children` is a read-only property that returns a live HTMLCollection of the child elements of Node.

[ParentNode.firstElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/firstElementChild)
 - The `firstElementChild` read-only property returns the object's first child `Element`, or null if there are no child elements.

[ParentNode.lastElementChild](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/lastElementChild)
 - The `lastElementChild` read-only property returns the object's last child `Element` or null if there are no child elements.

### ParentNode Methods
[ParentNode.append()](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/append)
 - The `append()` method inserts a set of Node objects or DOMString objects after the last child of the ParentNode. DOMString objects are inserted as equivalent Text nodes.

[ParentNode.prepend()](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/prepend)
 - The `prepend()` method inserts a set of Node objects or DOMString objects before the first child of the ParentNode. DOMString objects are inserted as equivalent Text nodes.

## [NonDocumentTypeChildNode](https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode)
The `NonDocumentTypeChildNode` interface contains methods that are particular to `Node` objects that can have a parent, but not suitable for `DocumentType`.

`NonDocumentTypeChildNode` is a raw interface and no object of this type can be created; it is implemented by `Element`, and `CharacterData` objects.

### NonDocumentTypeChildNode Properties
[NonDocumentTypeChildNode.nextElementSibling](https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode/nextElementSibling)
 - The `nextElementSibling` read-only property returns the `Element` immediately following the specified one in its parent's children list, or null if the specified element is the last one in the list.

[NonDocumentTypeChildNode.previousElementSibling](https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode/previousElementSibling)
 - The `previousElementSibling` read-only property returns the `Element` immediately prior to the specified one in its parent's children list, or null if the specified element is the first one in the list.

## [Document](https://developer.mozilla.org/en-US/docs/Web/API/document)
The `Document` object is made up of the HTML loaded into the `Window`.

The Document interface represents any web page loaded in the browser and serves as an entry point into the web page's content, which is the DOM tree. The DOM tree includes elements such as `<body>` and `<table>`, among many others. It provides functionality global to the document, like how to obtain the page's URL and create new elements in the document.

The Document interface describes the common properties and methods for any kind of document. Depending on the document's type (e.g. HTML, XML, SVG, …), a larger API is available: HTML documents, served with the text/html content type, also implement the `HTMLDocument` interface, whereas XML and SVG documents implement the `XMLDocument` interface.

### Document Methods
[document.createElement()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
 - In an HTML document, the `Document.createElement()` method creates the HTML element specified by `tagName`, or an `HTMLUnknownElement` if `tagName` isn't recognized.

[document.getElementByID()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
 - Returns a reference to the element by its ID; the ID is a string which can be used to identify the element; it can be established using the `id` attribute in HTML, or from script.

[document.getElementsByTagName()](https://developer.mozilla.org/en-US/docs/Web/API/document/getElementsByTagName)
 - Returns an `HTMLCollection` of elements with the given tag name. The complete document is searched, including the root node. The returned `HTMLCollection` is live, meaning that it updates itself automatically to stay in sync with the DOM tree without having to call `document.getElementsByTagName()` again.

[document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
 - Returns an array-like object of all child elements which have all of the given class names. When called on the document object, the complete document is searched, including the root node. You may also call `getElementsByClassName()` on any element; it will return only elements which are descendants of the specified root element with the given class names.

[document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
 - Returns the first `Element` within the document (using depth-first pre-order traversal of the document's nodes|by first element in document markup and iterating through sequential nodes by order of amount of child nodes) that matches the specified group of selectors.

[document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
 - Returns a list of the elements within the document (using depth-first pre-order traversal of the document's nodes) that match the specified group of selectors. The object returned is a `NodeList`.

## [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)
The `Element` interface represents an object of a `Document`. This interface describes methods and properties common to all kinds of elements. Specific behaviors are described in interfaces which inherit from `Element` but add additional functionality. For example, the `HTMLElement` interface is the base interface for HTML elements, while the `SVGElement` interface is the basis for all SVG elements.

Languages outside the realm of the Web platform, like XUL through the `XULElement` interface, also implement it.

### Element Properties
[Element.innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
 - The `innerHTML` property sets or gets the HTML syntax describing the element's descendants.

[Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
 - `classList` is a read-only property which returns a live `DOMTokenList` collection of the class attributes of the element.
 - `classList` itself is read-only, although you can modify it using the `add()`, `remove()`, and `toggle()` methods.

[Element.className](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)
 - `className` gets and sets the value of the class attribute of the specified element.

[Element.tagName](https://developer.mozilla.org/en-US/docs/Web/API/Element/tagName)
 - Returns the name of the element.

### Element Methods
[Element.getAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute)
 - `getAttribute()` returns the value of a specified attribute on the element. If the given attribute does not exist, the value returned will either be null or "" (the empty string).

[Element.setAttribute()](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)
 - Adds a new attribute or changes the value of an existing attribute on the specified element. Returns undefined.

## [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)
The `HTMLElement` interface represents any HTML element. Some elements directly implement this interface, others implement it via an interface that inherits it.

### HTMLElement Properties
[HTMLElement.style](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
 - The `style` property returns a `CSSStyleDeclaration` object that represents only the element's inline style attribute, ignoring any applied style rules.  See the CSS Properties Reference for a list of the CSS properties accessible via style.
 - Since the style property has the same (and highest) priority in the CSS cascade as an inline style declaration via the style attribute, it is useful for setting style on one specific element.

[HTMLElement.title](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/title)
 - The `title` property represents the title of the element, the text usually displayed in a 'tool tip' popup when the mouse is over the displayed node.

### HTMLElement Methods
[HTMLElement.click()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/click)
 - When `click()` is used with supported elements (e.g., one of the `input` types), it fires the element's click event. This event then bubbles up to elements higher in the document tree (or event chain) and fires their click events.
 - One exception: The `click()` method will not cause an `a` element to initiate navigation as if a real mouse click had been received.

## [HTMLSelectElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement)
The HTMLSelectElement interface represents a `select` HTML Element. These elements also share all of the properties and methods of other HTML elements via the `HTMLElement` interface.

### HTMLSelectElement Properties
[HTMLSelectElement.selectedIndex](https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement/selectedIndex)
 - `selectedIndex` is a long that reflects the index of the first selected `option` element (starting at 0). The value -1 indicates that no element is selected.

## [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
The `Event` interface represents any event which takes place in the DOM; some are user-generated (such as mouse or keyboard events), while others are generated by APIs (such as events that indicate an animation has finished running, a video has been paused, and so forth). There are many types of event, some of which use are other interfaces based on the main `Event` interface. `Event` itself contains the properties and methods which are common to all events.

### Event Properties
[Event.target](https://developer.mozilla.org/en-US/docs/Web/API/Event/target)
 - A reference to the object that dispatched the event. It is different from `currentTarget` when the event handler is called during the bubbling or capturing phase of the event.

[Event.currentTarget](https://developer.mozilla.org/en-US/docs/Web/API/Event/currentTarget)
 - Identifies the current target for the event, as the event traverses the DOM. It always refers to the element to which the event handler has been attached, as opposed to `target` which identifies the element on which the event occurred.

### Event Methods
[Event.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
 - Cancels the event if it is cancelable, without stopping further propagation of the event.

[Event.stopPropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation)
 - Prevents further propagation of the current event in the capturing and bubbling phases.

## [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)
`EventTarget` is an interface implemented by objects that can receive events and may have listeners for them.

`Element`, `document`, and `window` are the most common event targets; but other objects can be event targets too, for example `XMLHttpRequest`, `AudioNode`, `AudioContext`, and others.

### EventTarget Methods
[EventTarget.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
 - The `addEventListener()` method registers the specified listener on the `EventTarget` it's called on.

[EventTarget.removeEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
 - The `removeEventListener()` method removes the event listener previously registered with `addEventListener()`.

## [GlobalEventHandlers](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers)
The `GlobalEventHandlers` mixin describes the event handlers common to several interfaces like `HTMLElement`, `Document`, or `Window`.

### GlobalEventHandlers Properties
[GlobalEventHandlers.onclick](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onclick)
 - The `onclick` property returns the `click` event handler code on the current element.
   - When using `onclick`, you are only referencing the function name, not calling the function.
   - When using the `click` event to trigger an action, also consider adding this same action to the `keydown` event, to allow the use of that same action by people who don't use a mouse or a touch screen.

[GlobalEventHandlers.onchange](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onchange)
 - The `onchange` property is similar to `onclick`, except it fires for `input`, `select`, and `textarea` elements when a change to the element's value is committed by the user.
