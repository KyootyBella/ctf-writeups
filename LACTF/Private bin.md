MISC challenge @ LACTF feb 2023
made by: burturt
solved by: KyootyBella

# Initial stuff
As cybersecurity pioneers, we love to use end-to-end encrypted platforms so that even if we are hacked, the data is safe, right?

Actually, it turns out taking [https://github.com/scarsz/bin](https://github.com/scarsz/bin) and ripping out the XSS protection wasn't a good idea (hey, it was messing up sending html code!), as someone reported that they noticed some weird script running in some bin files! I've attached a copy so you can take a look.

In _completely unrelated news_, a certain 3-letter agency has told us that we need to get the contents of a certain paste someone uploaded. Problem is, it's kinda been deleted. Not to worry! While we promised no web logs, we have packet logs! I've already narrowed down the network traffic to only that user. Convenient that they were connected to our network, huh?

P.S. the bin server is still online if you need it. I have kinda forgotten the url though, sorry ¯\_(ツ)_/¯. It's hosted _somewhere_ under lac.tf, and I'm sure you can figure it out using the packet capture.

P.P.S. said 3-letter agency starts with an A, ends with an M, and has a C in it.

P.P.P.S. No, there is no admin bot, and no, you do not need to hack the website. This is a MISC challenge, not a web one.

we get two files sus-script.html and private-bin.pcapng.zip


# Let's get cracking

First we'll have a look at the pcap file as we need to figure out what website they are talking about, sadly everything is encrypted (daaamm security...) oh well, but we can still search for a domain name in our pcap file...

we then search for the string "lac.tf" cause we get told that it's on that domain and we can find this in a tcp packet telling us which server it's hosted at
![[1.png]]

This gives us access to a webserver which shows the files laying on it
![[2.png]]

hmmm sslkey?
Guess we can use that to decrypt our traffic, we'll download that down from the website and add it to our wireshark, so it uses that ssl key when reading the pcap file
https://www.comparitech.com/net-admin/decrypt-ssl-with-wireshark/

from here we can see we get even more http packets than before, this is because it has decrypted the traffic between the server and the user.

![[4.png]]

with this we can see there's some webpages that has been accessed, let's download those from our wireshark.
![[5.png]]

here we can then open the bin webpage that we have downloaded...
hmmm, asking for a decryption key??
![[6.png]]

we don't have a decryption key...
Let's check some more out...

what about that sus script we got at first?
![[7.png]]
After reading the script we can see something with a POST request, wait didn't it say something about a POST request in our pcap file?

surely enough in our pcap file there is a POST request and we have downloaded the file, let's go check it out...
![[8.png]]
it doesn't look like we can get some data out of it?

wait, the sus script adds it all to a zip file, let's rename the file into a zip file and see if we can extract the data.
![[9.png]]
surely enough, we got a key and some secret...
let's extract it via the password which is used in the script.

![[10.png]]
After extracting the key, we can now decrypt the bin!
![[11.png]]
and we got it!
flag.png let's download it!
![[flag.png]]

lactf{e2e_encryption_is_only_as_safe_as_the_client_1dc5f2}