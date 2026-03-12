Why I’m Building Tools for War Crime Investigation:

Thousands of videos and photos are uploaded to Telegram and Twitter every day from conflict zones. The problem isn't finding evidence; it's proving that what we’re looking at is real. As an engineering student, I realized that my most valuable contribution isn't just passion but building the technical "filters" that help investigators find the truth in a sea of data.
That's the reason I made this passion project "Digital Evidence Triage Tool"

1. Touching files for the first time is complicated 

In forensics, the most dangerous moment for a piece of evidence is the first time you touch it. If an investigator opens a file and accidentally saves a change, the metadata changes, and a defense lawyer could get that evidence thrown out of court. I tackled this by building a hashing system right into the start of my script. Before my code even looks at what’s in the file, it generates a SHA-256 hash. It’s like a digital fingerprint. If even one pixel is changed later on, that fingerprint breaks. I made sure the script reads the file in "chunks" (small 4KB blocks) so it doesn't crash a normal laptop when processing hours of heavy footage.

2. File headers instead of file names

One of the first things you learn in security is that file names are just labels, and labels lie. Anyone can rename a malicious script or a hidden document to evidence.jpg. I decided my tool shouldn't care about the file extension at all. Instead, I programmed it to look at the actual hex bytes at the very start of the file’s header. If the header says it’s a JPEG, the script treats it like one. If the header doesn't match the name, the script flags it as a "spoofed" file.


3. Turning Bytes into GPS data

Most people don't realize that their phones save GPS data in a weird format called "Rational" numbers—degrees, minutes, and seconds stored as fractions. It’s a mess to read. I built a converter into my tool that pulls these raw GPS coordinates and turns them into Decimal Degrees. This means an investigator can take the output of my script, drop it into Google Maps, and instantly see the exact street corner where the photo was taken. We’re also pulling the DateTimeOriginal from the EXIF data, showing exactly when the sensor captured the light.

4. Flagging for software

Finally, I added a check for "software signatures." If a photo has been through Photoshop, Canva, or GIMP, it leaves a trace. My script looks for these names. Now, just because a photo was cropped in Photoshop doesn't mean it’s a lie, but it does mean it’s no longer the original version. Identifying these edits immediately helps decide which photos can go to court and which ones need more technical analysis.

5. Next steps

This is just the beginning. Right now, the tool handles the "basics," but I’m looking into adding Error Level Analysis (ELA). This would allow the tool to look at how pixels are compressed to see if someone digitally added an object into a scene after the fact.

I’m not a lawyer or a field investigator yet, but I am an engineer. And in 2026, building the code that protects the integrity of the truth is one of the most important ways to fight for justice.
