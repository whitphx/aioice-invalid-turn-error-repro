# aioice-invalid-turn-error-repro

A reproduction of the error described in https://github.com/aiortc/aioice/issues/16.

```
pip install -r requirements.txt
python server.py
```

Open `http://localhost:8080` in your browser, select some options, then click "Start".
(This app is based on https://github.com/aiortc/aiortc/tree/main/examples/server .)

**The connection should fail** due to the invalid TURN server set to `RTCPeerConnection()` (see `server.py`),
while it should be fall back to the valid STUN configuration provided together.

My proposed fix is https://github.com/aiortc/aioice/pull/84 (https://github.com/whitphx/aioice/tree/ice-gathering-error-handling).
You can test it as follows:
```
pip uninstall aioice
pip install git+https://github.com/whitphx/aioice.git@ice-gathering-error-handling
```
