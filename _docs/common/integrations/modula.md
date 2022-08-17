
With [Modula](https://modula.twistapps.com/) integration you are given an easier way to manage your requests:
**placeholder for GIF showing the possibilities**


To use Request with Modula:
- add **RequestManager** to your scene<br />
`"+" > Modula > RequestManager`
- click "Add" on each request type you need to support with this manager
- in code, send requests simply by invoking `RequestManager.$RequestName$.Send(callback);`