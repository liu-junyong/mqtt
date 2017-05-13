# mqtt

An MQTT encoder and decoder,written in Golang.

This library was modified heavily from https://github.com/plucury/mqtt.go and
is API-incompatible with it.

Currently the library's API is unstable.

要达到 mqtt over websocket的效果，使用gorilla/websocket
两个库配合起来听别扭。

比如写入数据：

	b := new(bytes.Buffer)
	rc := mqtt.RetCodeAccepted
	connack := mqtt.ConnAck{
		ReturnCode: rc,
	}
	error := connack.Encode(b)
	if error != nil {
		logger.Info(error)
	}
	err := ws.WriteMessage(websocket.BinaryMessage, b.Bytes())
	if err != nil {
		...
    }
    
 挺别扭的   
 
 另外，通过 NextWriter 生成一个 ioWriter 看起来行，然而发不出数据。
 
