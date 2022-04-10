---
published: true

layout: post

title: Distinguishing Between Computer Viruses and Computer Worms

image: /images/michael-dziedzic-unsplash1.jpg
---

_How do you define a computer virus? how is this different to a computer worm? What role does encryption play in viruses and worms?_

![fuzzy computer screen]({{ site.baseurl }}/images/michael-dziedzic-unsplash1.jpg "computer viruses vs computer worms") 
_Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages){:target="_blank"}  on [Unsplash](https://unsplash.com/s/photos/computer-virus){:target="_blank"}_   

## Computer Virus
A computer virus is a malicious program that is triggered by an activation of some kind on a computer host. Viruses can replicate themselves, and they can take control of a victim’s computer, steal, manipulate or delete data. Viruses are often hidden in executable programs and scripts and occasionally non-executables such as documents. One of the first document viruses was the Melissa virus which infected a host when the malicious Microsoft Word document was opened. The virus would also email itself to the victims top 50 recipients in their Microsoft Outlook (FBI, 2019).  

## Computer Worm
A worm is a malicious program that can easily and quickly propagate itself to infect many computers systems in a short period of time. Whereas some action of a user is required to initiate a computer virus, worms can self-propagate over a network without the need for any user interaction or a triggering event. Worms will often use a remote code execution exploit as a way of spreading throughout a network. The first major attack on the internet was the Morris Worm in 1988. The worm used a remote exploit in the Finger and Mail services on Unix systems (FBI, 2018).  Modern malware uses elements of both worms and viruses. 
According to Rad et al. (2011, p. 113 – 114), the use of encryption in computer viruses is one of the most primitive approaches in concealing the operation of virus code. The first encrypted virus was CASCADE which appeared in 1988.  Encrypted viruses generally have two parts. There is the decryption loop code and the main encrypted body of the virus. The encryption hides the virus payload body. The encryption serves four main purposes:
1. To prevent static analysis of virus.
1. To prevent, or at least slow down investigators of the virus by making the process more difficult. 
1. To prevent tampering of the virus, or the creation of new variants. 
1. To escape detection by antiviruses which may implement string matching. 
