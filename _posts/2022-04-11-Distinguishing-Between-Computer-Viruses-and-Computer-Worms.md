---
published: true

layout: post

title: Distinguishing Between Computer Viruses and Computer Worms

image: /images/michael-dziedzic-unsplash1.jpg
---

_How do you define a computer virus? how is this different to a computer worm? What role does encryption play in viruses and worms? This quick post explains._

![fuzzy computer screen]({{ site.baseurl }}/images/michael-dziedzic-unsplash1.jpg "computer viruses vs computer worms") 
_Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages){:target="_blank"}  on [Unsplash](https://unsplash.com/s/photos/computer-virus){:target="_blank"}_   

## Definition of a Computer Virus
A computer virus is a malicious program that is triggered by an activation of some kind on a computer host. Viruses can replicate themselves, and they can take control of a victim’s computer, steal, manipulate or delete data. Viruses are often hidden in executable programs and scripts and occasionally non-executables such as documents. The first PC virus is considered to be [The Brain](https://en.wikipedia.org/wiki/Brain_(computer_virus)){:target="_blank"}, a boot sector virus which was released in 1986 by two brothers Basit and Amjad Farooq Alvi who were sick of customers making unauthorised copies of their software.  The virus contained a copyright message but did not perform any malicious actions. 

## Definition of a Computer Worm
A worm is a malicious program that can easily and quickly propagate itself to infect many computers systems in a short period of time. Whereas some action of a user is required to initiate a computer virus, worms can self-propagate over a network without the need for any user interaction or a triggering event. Worms will often use a remote code execution exploit as a way of spreading throughout a network. The first major attack on the internet was the [Morris Worm](https://en.wikipedia.org/wiki/Morris_worm){:target="_blank"} in 1988. The worm used a remote exploit in the Finger and Mail services on Unix systems.  Modern malware uses elements of both worms and viruses. 
## The use of encryption in computer viruses
According to [Rad et al. (2011, p. 113 – 114)](https://arxiv.org/ftp/arxiv/papers/1104/1104.1070.pdf){:target="_blank"}, the use of encryption in computer viruses is one of the most primitive approaches in concealing the operation of virus code. The first encrypted virus was [CASCADE](https://en.wikipedia.org/wiki/Cascade_(computer_virus)){:target="_blank"} which appeared in 1988.  Encrypted viruses generally have two parts. There is the decryption loop code and the main encrypted body of the virus. The encryption hides the virus payload body. Encryption serves four main purposes:
1. To prevent static analysis of virus.
1. To prevent, or at least slow down investigators of the virus by making the process more difficult. 
1. To prevent tampering of the virus, or the creation of new variants. 
1. To escape detection by antiviruses which may implement string matching. 
