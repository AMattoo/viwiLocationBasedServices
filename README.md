# Location Based Services based on ViWi Protocol
This is a proposal for location based services based on Volkswagen Infotainment Web Interface protocol.

I’m currently doing my bachelor’s degree in business informatics. I plan to do some kind of interface specification for by thesis based on the REST architecture pattern. These specified services should fit into an automotive environment. After some research regarding cars, infotainment systems and REST I found the submission of (i.a.) @wzr1337 that is public on www.w3.org (https://www.w3.org/Submission/viwi-protocol/). I really like this proposal because of its simplicity and beauty. I like the idea of the event driven async websocket approach combined with the classic REST concept.

After looking for some use cases to implement I found the github account (https://github.com/GENIVI) and confluence pages (https://at.projects.genivi.org/wiki/display/PROJ/Projects+Home) of GENIVI Alliance. They attracted my attention while I searched for some connectivity projects for cars.
On there confluence pages the team of the GENIVI described some use cases (https://at.projects.genivi.org/wiki/display/NAV/IVI+NavigationW3C) for navigation and location based services where they cooperate with the W3C. I thought it would be funny to take these use cases and specify an interface based on the viwi protocol submission and examine the difference between imperative/stateful approaches and a stateless one.

# MIT License

Copyright (c) 2017 j3ss5t

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
