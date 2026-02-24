---
sidebar_label: Meshtastic
---
## _"What is Meshtastic?"_
Meshtastic is an off-grid, decentralized mesh network built to run on low-power devices. It uses no cell towers or Wi-Fi routers, so it's not beholden to or at the mercy of corporations or governments, making it resistant to censorship campaigns, resilient to the ever more common outages of servers (like Amazon Web Services) or ISPs (like Spectrum), and totally subscription-free!

## _"What is a 'mesh network'?"_
Let's get visual!

The current 'hub and spoke' model is a network which resembles a bike wheel. At the center there is a 'hub' (or 'server') and 'spokes' (or 'clients') branching off around it in a circle. This model requires the 'spokes' to first communicate with the 'hub' to connect with another 'client'. This is how the current Web works and means the 'hub' (server) has the power to decide every connection.

A mesh network, by contrast, is one which there is no 'hub' meaning every 'spoke' (or, in our case, 'node') can freely communicate with every other one, with no one making decisions for anyone else. Unlike the situation where the hub goes down and everything goes down with it—like Amazon Web Services (AWS) knocking Netflix out or Spectrum cutting you off from your Signal / Delta Chat group chats—a mesh network is also _self-healing_, meaning if a node goes down or moves, the network dynamically adapts to ensure communications continue. This is what makes it resilient (and the ideal network style) in situations like natural disasters when cell towers fail.

## _"What is a node?"_
In abstract network terms, a node is an entity that can receive and transmit traffic. We can think about it sort of like a subway station with trains passing in and out (though, it's more like malleable slime mold than a fixed subway station, but you get it)!

In practical terms, it's the physical device known as a [transceiver] that provides the radio hardware to connect your smartphone to the other people on the network.

Some nodes even sport screens and keyboards so they can operate independently of your smart phone. Others hang out on towers to help connect distant nodes.

## _"How do I get started?"_
Meshtastic is one of the most straighforward mesh networks to implement. Designed around ease-of-use and simplicity, Meshtastic gets you up and running with little effort—install an app, pair a node, configure settings, and go! People nearby are most likely already using it, meaning you can join them in minutes!

Nodes (the transceivers we talked about earlier) can be purchased pre-configured with the necessary firmware (the instructions for how to link up lives) and the app can be installed on your smart phone via Google's Play Store or Apple's App Store (though, it's recommended to download the app anonymously from [F-Droid](https://f-droid.org/) or [Aurora Store](https://f-droid.org/en/packages/com.aurora.store/) instead to keep Google from snooping on you).


## What nodes should I get?
That's a big question in a short sentence. What is your use case? I'll list a few out. I am mainly listing OTS solutions, there are tons of builds out there, these are just the easiest. 
- EDC or Every Day Carry: I like the [T1000-e]() for EDC. It's small, tough, light, and can run for a couple days between charges if you turn off the GPS. As of writing it only works on Meshtastic and Meshcore. The [Heltec V4]() is another solid choice, It works on all 3 major meshes, though it uses more battery. It can easily be setup as a permanant MQTT gateway by connecting it to your home wifi.
- Car node: This is one that you attach outside of your car. If you have access to a 3d printer, you can build [something like this](https://www.printables.com/model/994724-low-profile-solar-meshtastic-car-node) using a [RAK Wisblock meshtastic starter kit]() a battery and solar panel listed on the build page. If you dont have a 3d printer, you can get a [Seed Solar P1]() and [some magnets]() to mount on the roof of you car.
- Solar node for static installations: The [Seed Solar P1]() is a solid setup, especially if you pair it with a [telescoping flag pole](). There are a few of these in GR zip tied to top floor apartment balconies. 

## What is the topology like?
The meshtastic flood routing algo will hear a message, if it still has hops left it will wait for X*random amount of time, subtract 1 from the hop count, retransmit the message if it is not one of the `_Mute` roles. X is a constant that is different for most roles. Infrastucture nodes have a lower X, client nodes have a higher X.
### But I thought meshtastic used directed routing?
It does, but only for direct messages. It still uses flood routing for talking in channels.
### What are the "Black Holes" I hear people talking about?
A black hole is what happens when someone sets their node to a role with a lower X than they should causing other nodes who might be in a better position to repeat to no retransmit because they already heard a repeat.
### What are the common roles and when should I use them?
#### The client roles
These are what 99% of the nodes out there should be using.
- Client_Mute: If you are in a city/suburban environment, use this for any node that is going to be on your person or inside a car/truck/home. It does not repeat and will not create routing holes.
- Client_Base: This is the role you want to use on your home tower, on top of your house, or in most situations where you're in an sub 100ft HAAT location. This is a semi-infrastructure role
- Client: Use this in locations where you want the node to repeat, but after the infrastucture nodes have had time to transmit. Use this for your MQTT gateways and for mesh nodes mounted *outside* the car.
#### The infrastucture roles
These should only be used if you are at least 100ft [HAAT](https://recnet.com/haat). If using the calculator, put in your lat/long, put in your antenna height above ground level (it will get the elevation above sea level for you), and select the `Above Ground Level` radio button, then get HAAT. 
- Repeater: Use this if you have a great location (greater than 500ft HAAT), dont a screen, and need prioritized routing. These are AND statements, if one doesnt apply to you, dont use this role. This role will not show up in your node lists.
- Router_Late: Use this if you have an OK location (100-500ft HAAT), and need prioritized routing. These are AND statements, if one doesnt apply to you, dont use this role.



