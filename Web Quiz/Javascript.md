**Script tag**
`<script src="..." />`
* The script downloaded/executed as soon as the HTML parser finds the tag.  
* Poor - The **HTML parsing** is **blocked** while the script is being **downloaded and executed**.
	
`<script src="..." async />`
* The script is downloaded in parallel to parsing the page, and executed as soon as it is available.
* The **HTML parsing** is **blocked** while the script is being **executed**.

`<script defer src="..." />`
- The script will be downloaded in parallel to parsing the page, and executed after the page has finished parsing.
- The **HTML parsing** is **never blocked**.

**Rendering Pipeline & Compositing**
- DOM + CSSOM = Render tree

**Call Stack & Event Loop**
- Call Stack
	- Keeps track of the function calls and their execution contexts
- Web API
	- Extends the builtin JS features (ex: DOM manipulation, timers, fetch api)
	- Called by the Call Stack when needed
* Macrotask Queue
	* Timers (setTimeout/setInterval)
	* User input events and UI rendering tasks 
* Microtask Queue
	* Promises
* Event Loop
	* Loop that continuously sends the /micro tasks from the queue to the call stack
	* http://latentflip.com/loupe
* Order of execution
	* Sync (call stack) -> Async (microtask queue) -> Timers (macrotasks queue)

**Resolving Domain Requests**
- Browser sends a request
	- 1. Recursive DNS Resolver -> Root Name Server (Top Level Domain Name Server IP address)
	- 2. Recursive DNS Resolver -> Top Level Domain Name Server (Authoritative Name Server IP address)
	- 3. Recursive DNS Resolver -> Authoritative Name Server (website's IP address)
