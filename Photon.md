# PUN : how to send custom events

```csharp
using Photon.Pun;
using Photon.Realtime;
using ExitGames.Client.Photon;

public class ExampleObject {
	public void EventSender() 
    {
        // Event Identifier
		byte evCode = 0;
    
        // send Data
        object[] content = new object[] 
        {
            new Vector3(0, 10, 5),
            5
        }; 
    	
    
		RaiseEventOptions raiseEventOptions 
            = new RaiseEventOptions { 
            Receivers = ReceiverGroup.All };
// Receivers.ReceiverGroup.All
// Send Event to All Clients
        
// Receivers.ReceiverGroup.Other
// Send Event to All client Except Me
        
// Receivers.ReceiverGroup.MasterClient
// Send Event to MasterClient
        
		SendOptions sendOptions 
            = new SendOptions {  
            Reliability = true };
// Reliability = true: DeliveryMode.Reliable
// Reliability = false: DeliveryMode.Unreliable

// Channel = (byte) : default is 0
// Set DeliveryMode : Reliable, Unreliable, ReliableUnsequenced, UnreliableUnsequenced
        
// Encrypt = (bool) : default is false (암호화)
		
        // send Data
        PhotonNetwork.RaiseEvent(evCode, content, raiseEventOptions, sendOptions);
	}
}
```