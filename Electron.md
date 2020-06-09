Some notes on electron

### IPC vs Socket.io

Might be worth investigating performance tradeoffs.

communication between the renderer (electron browser window that shows ui) and the backend capture code is happening over socket.io. This is an artifact from the WebUI centered version. This works seamlessly in electronjs by using `loadURL` rather than just an index file. When  using a index file with `file://` based loadURL socketio does not load. We could either load the socket io client js a different way or switch off socketio and use electrons built in `ipc` event handlers.Mattermost's electronjs based client use `ipc` and `ipcRender` emit and event handlers (see `app.js`, `index.jsx` and `MainWindow.jsx`)