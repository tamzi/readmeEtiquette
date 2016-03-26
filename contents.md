Most READMEs are way too verbose or have few words to it. 
A README is the first file a person should read when encountering a source tree, and it should be written as a very brief, very basic introduction to the software. 

It should contain:
 - the name of the code, 
 - the version, 
 - possibly last date updated, and 
 - a very brief, high-level overview of the software (very high-level). 
 
 And that's all, other than possibly references to which files contain other information that a person might be interested in i.e.
  - installation instructions (in INSTALL), 
  - the authors (in AUTHORS), or 
  - history (in ChangeLog or ReleaseNotes).

The README is an introduction. 
It should assume the reader knows absolutely nothing about the software and should provide a brief introduction. If software were a screenplay, the README would be the 10 second tagline used to pitch the script to a producer. 

If a person finishes reading the first 10 lines of frobnicator/README and does not know if frobnicator is a widget library, accounting software, or a video game, then the author of the README has failed.



A README should be simple and short, but a good README can save time especially if it's for something like command-line parameter parsing library.

Here's what I think it should include:
•name of the projects and all sub-modules and libraries (sometimes they are named different and very confusing to new users)
•descriptions of all the project, and all sub-modules and libraries
•5-line code snippet on how its used (if it's a library)
•copyright and licensing information (or "Read LICENSE") 
•instruction to grab the documentation
•instructions to install, configure, and to run the programs
•instruction to grab the latest code and detailed instructions to build it (or quick overview and "Read INSTALL")
•list of authors or "Read AUTHORS"
•instructions to submit bugs, feature requests, submit patches, join mailing list, get announcements, or join the user or dev community in other forms
•other contact info (email address, website, company name, address, etc)
•a brief history if it's a replacement or a fork of something else
•legal notices (crypto stuff)

Apache HTTP Server has a simple yet good README. Another good one I found available online is GNU Make's README.

As per formatting, I would say stick to the Unix traditions as much as possible, and/or use markdown especially for github projects, which renders README.md as html.
•ASCII characters only, if the README is written in English
•write it in English if possible, and ship translated version with two-letter language code extension like README.ja
•80 characters or less per line
•single empty line between paragraphs
•dashes under the headers
•indent using whitespace (0x20) not tab

Putting it all together...
Documentation
-------------

GNU make is fully documented in the GNU Make manual, which is contained
in this distribution as the file make.texinfo.  You can also find
on-line and preformatted (PostScript and DVI) versions at the FSF's web
site.  There is information there about ordering hardcopy documentation.

  http://www.gnu.org/
  http://www.gnu.org/doc/doc.html
  http://www.gnu.org/manual/manual.html 



Wikipedia defines as:

A readme (or read me) file contains information about other files in a directory or archive and is very commonly distributed with computer software.

and it lists the following contents:

•configuration instructions
•installation instructions
•operating instructions
•a file manifest
•copyright and licensing information
•contact information for the distributor or programmer
•known bugs
•troubleshooting
•credits and acknowledgements
•a changelog
 
