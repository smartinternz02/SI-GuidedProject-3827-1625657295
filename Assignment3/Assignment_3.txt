import wiotp.sdk.device
import time
import random
myConfig = { 
    "identity": {
        "orgId": "8afe2a",
        "typeId": "IOTCHETAN",
        "deviceId":"11042002"
    },
    "auth": {
        "token": "Chetan@12344321"
    }
}

def myCommandCallback(cmd):
    print("Message received from IBM IoT Platform: %s" % cmd.data['command'])
    m=cmd.data['command']

client = wiotp.sdk.device.DeviceClient(config=myConfig, logHandlers=None)
client.connect()

while True:
    Water=random.randint(0,100)
    Light=random.randint(0,100)
    myData={'Water':Water, 'Light':Light}
    client.publishEvent(eventId="status", msgFormat="json", data=myData, qos=0, onPublish=None)
    print("Published data Successfully: %s", myData)
    client.commandCallback = myCommandCallback
    time.sleep(2)
client.disconnect()
