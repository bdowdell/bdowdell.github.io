---
layout: post
title: "New ThinkPad!"
---

I recently purchased my first new computer in 9 years, and I got a Lenovo
ThinkPad P1 Gen 3! My previous laptop was a 2012 MacBook Pro I bought halfway
through graduate school. The MBP was a great laptop and it still functions, but
it has defintely started to show its age. I swapped out the internal hard drive
a few years back with a solid-state drive, but with only 4 GB of memory and a
tired battery, it was definitely becoming difficult to use as an effective tool.

I've been using MacBooks since 2007 and was initially planning on getting a new
M1 MBP, or maybe the M1 MacBook Air as a replacement. The new M1 system on a chip seems to
promise very impressive performance, but I ultimately was hesitant about being
an early-adopter. As a data scientist, I rely on Anaconda's Python distribution
and officially it hasn't been ported to the new M1 architecture yet. There are
several workarounds, either using miniconda or running anaconda under emulation,
but neither seem perfect solutions yet. I think based on the performance
benchmarks I've seen, data science workflows will absolutely benefit from
Apple's M1 architecture, but I'm not quite ready to make that jump.

In addition to my concerns over using my data science stack on the new M1, the
reality is that I spend upwards of 95% of my time working in a Linux
environment. Dual-booting Linux on the M1 is a problem that has not been solved,
and while I could work acceptably well using MacOS, I just really prefer Linux.
Buying a new M1 MBP just didn't seem to make sense if I couldn't reliably dual
boot Linux. I like MacOS a lot, but there aren't any benefits to using it over
Linux. If I needed to do serious photo, video, or audio editing using Photoshop, Final
Cut Pro, or Logic Pro, I would definitely want to be using MacOS.

![thinkpad_cover]({{site.url}}/assets/img/ThinkPad/thinkpad_cover.jpg)

## So why Lenovo? Why a ThinkPad?

Around the same time that I started researching the new Apple M1 laptops, my
employer deployed new laptops at work as a result of a recent merger and digital
transformation goals. Guess what? They sent us Lenovo ThinkPads (the P1 Gen 3 to
be specific). I've had limited experiences with ThinkPads, but I can remember my
dad bringing one home from work in the 1990s (they were IBM ThinkPads at that
time), and that was the first time I ever used a laptop. As I started using my
new work ThinkPad, I became very impressed with it to the point that I began to
investigate them as an alternative to replacing my aging MBP.

I specified a ThinkPad P1 Gen 3 with a healthy build sheet:

* 10<sup>th</sup> generation Intel Core i7-10750H
* 1 TB SSD internal drive
* 64 GB DDR4 memory
* Nvidia Quadro T2000 with Max-Q
* 15.6" FHD display (1920x1080)
* Windows 10 Home Edition + Microsoft 365 Personal

Mostly, I focused on maxing out performance. While Intel's Core i9 was an
option, I think the additional cost may not have justified the performance
boost. I selected as  much memory as could be configured and the Quadro T2000
over the T1000 for the additional CUDA cores. I did select the base dispaly
because I won't be needing ultra high-definition resolution. The top display
would also likely signficiantly erode battery life, and the midrange display
included an infrared camera that doesn't seem to work well with most Linux
distributions. I will use the ThinkPad primarily for data analysis, coding, and
software engineering, so high-end visuals aren't necessary.

Unlike MacBooks, the ThinkPad's bottom cover can be removed and the components
can be upgraded over time. There is also space for a second internal SSD so I
can add more storage if needed. Apple has long since done away with a removable
bottom cover (my 2012 MBP was one of the last with that capability), and all of
the components are soldered to the motherboard so upgrades are not really
feasible.

I did opt to have Windows 10 pre-installed because there are times where it is
handy to have Windows. When working in Linux, I use LibreOffice, but it is also
handy to have access to Office 365.

As I started to read ThinkPad P1 Gen 3 reviews, I became slightly concerned
about the battery life. Between the Core i9, UHD 4K display, and Quadro T2000
GPU, the reported battery life was a bit dismal. This is another reason I opted
for the Core i7 over the Core i9 and the base FHD display over the 4K UHD.
Realistically, I will likely not require the max power when I'm not on AC charge.

![thinkpad cover
closeup]({{site.url}}/assets/img/ThinkPad/thinkpad_cover_closeup.jpg)

## The waiting begins

I placed my order on March 16<sup>th</sup> and the intial shipping estimate put
it at my door in mid May! There is a world-wide shortage of laptop dispay glass
and other components currently, as well as extra complications brought on by the
ongoing COVID-19 pandemic. For being the first computer I've purchased in 9
years, I was super anxious and mid-May felt like a year away.

Fortunately, I didn't have to wait quite so long. My ThinkPad was shipped from
China on April 2<sup>nd</sup> and arrived at my doorstep on April
14<sup>th</sup>! As I write this, I've had my new ThinkPad for about four days,
and so far, I have been very pleased. After opening it up, I went through the
intial Windows 10 set up, which was very easy and relatively quick.

In the time between ordering and receiving my ThinkPad, I had time to think
about which Linux distribution I wanted to install alongside Windows 10. My MBP
dual-boots Ubuntu 18.04 LTS, while my 10 year old desktop runs SparkyLinux 5. I've tended to
stay within the Debian family, but I'm always curious to try something new.
However, I knew I needed a distribution that would work well with the current
Nvidia drivers for GPU computing. That requirement steered me towards Ubuntu,
but I've never really been crazy about Ubuntu post-Unity. I still use it, but it
doesn't stir any deep connection with the experience.

Then, I came across System76's Pop! OS, which offers the stability and ease of use of Ubuntu but
with special focus towards scientific and engineering computing. What
specifically caught my eye is that Pop! offers support for Nvidia drivers at
install. Obviously, Nvidia drivers can be installed even if they aren't natively
supported, but I like when things *just work* (which is arguably not *the way*
in Linux).

Beyond merely having Nvidia support, Pop! has different graphics mode: Integrated, Nvidia,
Hybrid, and Compute. This is exciting because it means I can reserve all of
Nvidia's GPU power for computing when I need it and not waste any of it on
running the display. This also helps conserve battery life by not using the GPU
to power the display. Currently I've been running under Hybrid mode which
prefers the integrated graphics unless the Nvidia GPU is specified, and it has
worked well. The integrated mode turns off the Nvidia GPU which will result in
maximum battery life, while the Compute mode keeps the Nvidia GPU on but keeps
it purely reserved for computing (like with TensorFlow and PyTorch).

![thinkpad]({{site.url}}/assets/img/ThinkPad/thinkpad_open.jpb)

## My impression so far

In short, I am really pleased with my new Lenovo ThinkPad. From an aesthetics
perspective, I really like the matte black carbon fiber body with the little
hints of red to tie in to the iconic TrackPoint.

So far, battery life has been much better than I expected, primarily because I
am not really using the Nvidia GPU off of AC power, and I'm keeping the screen
relatively dim and the keyboard backlighting off unless I need it.

Although the ThinkPad P1 Gen 3 is a larger form-factor than my previous 2012
MacBook Pro (15.6" versus 13"), it is a slimmer and lighter laptop than my old
MBP. At just a little over 3 pounds in weight, it is portable and easy to carry
around but also feels very sturdy. Considering the horsepower, it's an
impressive package.

The keyboard is excellent. Lenovo knows how to make a great keyboard. A lot of
people complain about the placement of the Fn & Ctrl keys on the bottom left,
but it doesn't bother me.

The trackpad is very nice, but what I have been pleasantly surprised with is
the TrackPoint! I absolutely love using the little red dot in the middle of the
keyboard for moving the mouse around the screen. The TrackPoint uses pressure
instead of motion to guide the mouse. Using the TrackPoint doesn't require my
hands to move far from home position and makes switching between typing and
navigating quicker. The middle-mouse (or keystone) button between the left and
right mouse button enables scrolling with the TrackPoint. But what is really
awesome is how easy it is to use the middle-mouse button to paste in a terminal
after selecting text. I'm a TrackPoint convert, now!

![trackpoint]({{site.url}}/assets/img/ThinkPad/thinkpad_open_trackpoint_focus.jpg)

Using Pop! OS 20.04 LTS so far has also been a positive experience. I'll write a
little more about it in a separate post, but all of the ThinkPad hardware works
as expected, including the finger print reader. I really love it when things
*just work*!

