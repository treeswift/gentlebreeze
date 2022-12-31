# The GentleBreeze project

_11 And he said, Thou shalt go forth tomorrow, and shalt stand before the Lord in the mount; behold, the Lord will pass by. And, behold, a great and strong wind rending the mountains, and crushing the rocks before the Lord; but the Lord was not in the wind; and after the wind an earthquake; but the Lord was not in the earthquake:_

_12 and after the earthquake a fire; but the Lord was not in the fire: and after the fire the voice of a gentle breeze._

3 Kings 19 (the Brenton Septuagint translation)

## Concept

The core idea of GentleBreeze is data transmission (particularly, internet sharing) via ephemeral media — i.e. physical media that are not normally placed behind logical network interfaces.

Consider a flip phone that misses the functionality of a network hotspot or that has the hotspot disabled despite being otherwise lawfully unlocked (a real world case). Or consider a smartwatch not offering the hotspot feature "because it would drain the battery", no matter how sparingly you are prepared to use it. Or. Or.

With the rushed adoption of the 5G spectrum and the impending 3G sunset 80% of the mobile phones in the United States suddenly turned into pocket PCs. If you still want to use your old phone, you need another one to keep it connected on the go.
One possible solution is a Wi-Fi hotspot (you can find one for $10..$15, or even cheaper), but such devices aren't capable of voice calling, and forwarding incoming calls via Wi-Fi (e.g. via a SIP connection) is unreliable (keywords: "push notifications").
Another possible solution is to use a $20..$25 flip phone for calling and texting (directly or via a Bluetooth audio and/or a remote control Wi-Fi connection) and your favorite smartphone for the rest (i.e. data).
However, the flip phone is not necessarily capable of (or configurable for) sharing its internet connection. It may need our help.

Fortunately,

* both on Android and on Windows 10 (including Windows Mobile 10) it's possible to install a tunnel client (a tiny app that picks up local traffic and packs ("multiplexes") it into a single point-to-point connection) in userspace without hacking the kernel. These APIs have been designed for VPN clients, but the "V" is not a requirement. (iPhone users are on their own, for now. Don't dare leave your walled garden!)
* a tunner server — the tiny app that unpacks ("demultiplexes") the serial connection into multiple regular IP connections into the greater Internet — can be a regular userspace app and even a Javascript-enabled browser page.
* access to camera and microphone (necessary to consume data transmitted over video, via an audio cable or via pure open air) needs user permission, but it's a common and typical application permission, easy to request and easy to grant.

## Implementation

Our train of thought can be followed via the Issues page.

Links to component projects (in their own programming languages, and *possibly* under their own licenses, though we'll make our best to keep as much as possible in the public domain) will appear here.

### Progress: end of 2022

As we explore multiple alternative media, the present breakdown of [issues](../../issues) has partly gotten out of sync.
Our 2022 achievements, however, are as follows:

* TUN exit node (Android) -- parsing low-level ICMP request and re-packaging high-level ICMP response (ping).
* TUN exit node (browser) -- no such thing is presently possible by itself, but there are VPN exit nodes on the web supporting e.g. Wireguard via WebRTC.
* Audio (air) -- phase modulation, carrier detection and symbol boundary detection.
* Audio (cable) -- refined a working (Nexus 5 -- Moto Z3) full duplex attenuator circuit for UART or pseudo-UART: ~24 kOhm in, ~2.2 kOhm out; no semiconductors, inductors or capacitors.

Our current roadblocks/impediments are as follows:

* MTP without Android extensions -- tested. Protocol limitations disallow partial file modification. Together with Javascript File API limitations it effectively renders the MTP channel unusable (unless it's possible to index a file while it is being transfered).

Our present research is in the following areas:

* Bluetooth -- recent versions of Android and W10M support BLE server profiles, but not all profiles are available to applications. (Will a Qualcomm BREW device offer greater control?)
* Audio (air) -- Viterbi or Fano?

## Legal

Nothing in this project should be understood as a means of circumventing the contractual restrictions placed on data connection sharing any more than reading aloud from a lawfully obtained book copy circumvents the end user license agreement implicitly binding the book buyer, or any more than smelling cooking meat amounts to eating it. The maximum realistic data transmission speed achievable via an audio channel, without going ultrasound, is a few kilobits per second; for a video channel, assuming a sharp high-resolution transmitter screen, it is tens of kilobytes per second — barely enough to open a banking app or check mail, and a tiny fraction of data transmission speeds normally offered by 4G LTE. One would achieve much greater connection sharing bandwith (albeit with poorer latency) by simply downloading music or photos onto a phone and sharing them over MTP.

At the same time, no technological consideration should obscure a principled one. For that reason, each of the phone plans we ourselves use for testing purposes explicitly includes an internet hotspot / internet sharing / connection sharing service, and we advise you to do the same. _Good_ carriers (no name calling, though the leading initial is 'U') offer data sharing with every plan, and it adds less to your bill than those annoying fees charged by Uncle Sam.

Also, this is not a good way to copy data from enterprise or government networks. You will get caught and spend the rest of your days in Moscow.
