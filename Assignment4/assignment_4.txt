import wiotp.sdk.device
import time

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
    print()

client = wiotp.sdk.device.DeviceClient(config=myConfig, logHandlers=None)
client.connect()

while True:
    client.commandCallback = myCommandCallback
    time.sleep(2)
client.disconnect()
