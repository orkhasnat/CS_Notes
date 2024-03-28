Awesome Console Services
===
Source: [Github](https://github.com/chubin/awesome-console-services)
A curated list of awesome console services (reachable via HTTP, HTTPS and other network protocols).

---
Table of Contents
===
- [[Awesome Console Services#IP Address|IP Address]]
	- [[Awesome Console Services#DNS|DNS]]
	- [[Awesome Console Services#JSON only|JSON only]]
- [[Awesome Console Services#Geo-location|Geo-location]]
- [[Awesome Console Services#Text Sharing|Text Sharing]]
- [[Awesome Console Services#URL Shortener|URL Shortener]]
- [[Awesome Console Services#File Transfer|File Transfer]]
- [[Awesome Console Services#Tools|Tools]]
- [[Awesome Console Services#Cryptography|Cryptography]]
- [[Awesome Console Services#Monitoring|Monitoring]]
- [[Awesome Console Services#Weather|Weather]]
- [[Awesome Console Services#News|News]]
	- [[Awesome Console Services#COVID-19|COVID-19]]
- [[Awesome Console Services#Map|Map]]
- [[Awesome Console Services#Money|Money]]
- [[Awesome Console Services#Documentation|Documentation]]
- [[Awesome Console Services#Dictionaries and translators|Dictionaries and translators]]
- [[Awesome Console Services#Generators|Generators]]
- [[Awesome Console Services#Entertainment and Games|Entertainment and Games]]
	- [[Awesome Console Services#Curl Based|Curl Based]]
	- [[Awesome Console Services#Telnet/SSH Based|Telnet/SSH Based]]
- [[Awesome Console Services#Scripts|Scripts]]
- [[Awesome Console Services#Clients|Clients]]

---
## IP Address
#### Inline
- `curl l2.io/ip`
- `curl https://echoip.de`
- `curl ifconfig.me`
- `curl ipecho.net/plain`
- `curl -L ident.me` 
	- They have an [api endpoint](http://api.ident.me) as well.
- `curl -L canihazip.com/s`
- `curl -L tnx.nl/ip`
- `curl wgetip.com`
- `curl whatismyip.akamai.com`
- `curl ip.tyk.nu`
- `curl bot.whatismyipaddress.com`
- `curl curlmyip.net`
- `curl api.ipify.org`
- `curl ipv4bot.whatismyipaddress.com`
- `curl ipcalf.com`

#### New line
- `curl ipaddy.net`
- `curl eth0.me`
- `curl ipaddr.site`
- `curl ifconfig.co`
- `curl ifconfig.pro`
- `curl curlmyip.net`
- `curl ipinfo.io/ip`
- `curl icanhazip.com`
- `curl checkip.amazonaws.com`
- `curl smart-ip.net/myip`
- `curl ip-api.com/line?fields=query`
- `curl ifconfig.io/ip`
- `curl -s ip.liquidweb.com`
- `curl ifconfig.es`
- `curl ipaddress.sh`
- `curl 2ip.ru`

### DNS
- `dig @1.1.1.1 whoami.cloudflare ch txt +short` (IPv4)
- `dig @2606:4700:4700::1111 whoami.cloudflare ch txt -6 +short` (IPv6)
- `dig @ns1.google.com o-o.myaddr.l.google.com TXT -6 +short` (IPv6)
- `dig @ns1.google.com o-o.myaddr.l.google.com TXT -4 +short` (IPv4)
- `dig resolver.dnscrypt.info TXT +short`
- `curl https://dnsjson.com/resolver.dnscrypt.info/TXT.json`
- `curl -L https://edns.ip-api.com/json`
- `curl 'api.hackertarget.com/zonetransfer/?q=zonetransfer.me'` DNS Zone Transfer

### JSON only
- `curl httpbin.org/ip`
- `curl wtfismyip.com/json`
- `curl -L iphorse.com/json`
- `curl geoplugin.net/json.gp`
- `curl https://ipapi.co/json`
- `curl -L jsonip.com`
- `curl gd.geobytes.com/GetCityDetails`
- `curl ip.jsontest.com`

## Geo-location
- `curl ipinfo.io/8.8.8.8` 
- `curl ipinfo.io/8.8.8.8/loc`
- `curl ip-api.com` 
- `curl ip-api.com/8.8.8.8`
- `curl ifconfig.co/country`
- `curl ifconfig.co/city`
- `curl ifconfig.co/country-iso` 
- `curl ifconfig.co/json`
- `curl ifconfig.es/geo`
- `curl ifconfig.es/json`
- `curl ifconfig.es/country`
- `curl ifconfig.es/code`
- `curl ifconfig.es/city`
- `curl ifconfig.es/latitude`
- `curl ifconfig.es/longitude`

## Text Sharing
- `echo "Hello world!" | curl -F 'f:1=<-' ix.io`
- `echo "Hello world!" | curl -F file=@- 0x0.st`
- `echo "Hello world!" | curl -F 'clbin=<-' https://clbin.com`
- `echo "Hello world!" | nc termbin.com 9999`
- `echo "Hello world!" | curl -F 'sprunge=<-' sprunge.us`
- `echo "Hello world!" | curl -H "content-type: text/plain" -d @- https://textdb.dev/api/data/unique-id-for-my-text`
- `curl https://patchbay.pub/your-custom-path -d "Hello world!"` and `curl -s https://patchbay.pub/your-custom-path`

## URL Shortener
- `curl -s tinyurl.com/api-create.php?url=<link>`
- `curl https://is.gd/create.php?format=simple&url=<link>`
- `curl -F shorten=<link> https://0x0.st`
- `curl -F url=<link> https://shorta.link`

## File Transfer
- `curl --upload-file <file> transfer.sh/<filename>`
- `curl -F file=@<file> https://ttm.sh`
- `curl https://patchbay.pub/your-custom-filepath.exe --data-binary @<file>` and `curl -LO https://patchbay.pub/your-custom-filepath.exe`
- `nc oshi.at 7777 < <file>` 
- `curl https://oshi.at -F f=@<file>`
- `curl -F file=@<file> https://0x0.st`
- `curl -F file=@<file> https://api.anonfile.com/upload`

## Tools
- Create QR-code for a string ([chubin/qrenco.de](https://github.com/chubin/qrenco.de))
	- `curl qrenco.de/STRING`
	- `echo STRING | curl -F-=\<- qrenco.de`
- Convert a document ([source](https://github.com/docverter/docverter))
	- `curl "http://c.docverter.com/convert" -F from=html -F to=pdf -F "input_files[]=@your-file-name.html" -o "output-file-name.pdf"`
- Title/URL of latest upload from indicated YouTube channel
	- `curl -s "https://decapi.me/youtube/latest_video?user=NPR"`
- Last tweet from indicated account
	- `curl -s "https://decapi.me/twitter/latest?name=NPR"`
- Check if indicated twitch channel is online
	- `curl -s "https://decapi.me/twitch/uptime?channel=IGN"`
- HTTP request and response Service (e.g. send response after 4 seconds)
	- `curl -s "https://httpbin.org/delay/4"`
- HTTP response defined in the request parameters
	- `curl -s "https://urlecho.appspot.com/echo?body=Hello+World"`
- HTTP proxy makes new requests based on input parameters
	- `curl -s "https://urlreq.appspot.com/req?method=GET&url=https://l2.io/ip"`
- TCP port scan using NMAP
	- `curl -s "https://api.hackertarget.com/nmap/?q=93.184.216.34"`
- Extract all links from a page
	- `curl -s "https://api.hackertarget.com/pagelinks/?q=msn.com"`
- Whois lookup
	- `curl -s "https://api.hackertarget.com/whois/?q=google.com"`
- Useful tool to retrieve fake api data
	- `curl -s "https://jsonplaceholder.typicode.com/users"`

## Cryptography
- SSL fingerprint search 
	- `curl https://ja3er.com/search/535886c8d0a1b14f02298967bb990171`

## Monitoring
- `curl ping.gl`
- Check status pages of common services
	- `curl https://status.plaintext.sh/t`

## Weather
- `curl wttr.in` or `curl wttr.in/Berlin` 
- `finger oslo@graph.no`
- `nc rainmaker.wunderground.com 3000` (also works with telnet)
- METAR from the specified ICAO
	- `curl https://tgftp.nws.noaa.gov/data/observations/metar/stations/KAAO.TXT`

## News
- Fetch the latest news
	- `curl getnews.tech/world+cup`
- [Hacker News feed](github.com/NalinPlad/hkkr.in)
	- `curl hkkr.in`
- Exploring (crypto)currencies exchange rates
	- `curl rate.sx`
- News aggregator
	- `gopher://gopher.leveck.us:70`
- Reddit Gopher
	- `gopher://gopherddit.com:70`
- Reddit in terminal (ssh + text browser)
	- `ssh redditbox.us`
- Hacker news
	- `gopher://hngopher.com:70`
#### COVID-19
- `curl https://corona-stats.online`
- `curl -L covid19.trackercli.com`
- Covid-19 statistics for your country
	- `curl snf-878293.vm.okeanos.grnet.gr`

## Map
- Show a zoomable world map
	- `telnet mapscii.me` ***DOPE***

## Money
- Get cryptocurrencies exchange rates
	- `curl rate.sx`
- Get BTC/USD exchange rate (also works with telnet)
	- `nc ticker.bitcointicker.co 10080`
- Get stock visualizer and tracker
	- `curl https://stonks.icu/amd/msft`
- Get stocks prices and information for provided yahoo ticker
	- `curl terminal-stocks.shashi.dev/:ticker`
- Cryptocurrency tracking TUI ([source](https://github.com/miguelmota/cointop))
	- `ssh cointop.sh`

## Documentation
- UNIX/Linux commands cheat sheets using curl ([chubin/cheat.sh](https://github.com/chubin/cheat.sh))
	- `curl cheat.sh`
- Subnet calculator
	- `curl 'https://api.hackertarget.com/subnetcalc/?q=192.168.1.0/24'` 
- NPA/NXX Lookup
	- `gopher://telcodata.us:70`
- All known gopher servers
	- `gopher://gopher.floodgap.com/1/world`

## Dictionaries and translators
- `curl 'dict.org/d:command line'`

## Generators
- Generate random commit message
	- `git commit -m "$(curl -sk whatthecommit.com/index.txt)"`
* Generate random number
	* `curl "https://www.random.org/integers/?num=1&min=1&max=100&col=1&base=10&format=plain&rnd=new"`
- Fuck off as a service
	- `curl -H 'Accept: text/plain' https://foaas.com/cool/:from`
- Generate a pseudo random (American?) name ([treyhunner/pseudorandom.name](https://github.com/treyhunner/pseudorandom.name))
	- `curl pseudorandom.name`
- Random jokes
	- `curl https://icanhazdadjoke.com`
- GUID
	- `curl givemeguid.com`
- IT excuses (also works with telnet)
	- `nc towel.blinkenlights.nl 666`
- Generate text using the GPT2 AI model from a seed string
	- `curl -s 'https://api-inference.huggingface.co/models/distilgpt2' --data-raw '"what is the meaning of life?"' | jq '.[].generated_text'`

## Entertainment and Games
##### Curl Based
- Watch Star Wars in terminal via curl ([source](https://github.com/martinraison/ascii-tv)) 
	- `curl https://asciitv.fr`
- Watch Star Wars in terminal via netcat (also works with telnet) 
	- `nc towel.blinkenlights.nl 23`
- Chat over SSH ([shazow/ssh-chat](https://github.com/shazow/ssh-chat)) 
	- `ssh chat.shazow.net`
- SSH chat client ([source](https://git.causal.agency/catgirl)) 
	- `ssh chat@ascii.town`
- Display an animated party parrot ([hugomd/parrot.live](https://github.com/hugomd/parrot.live)) 
	- `curl parrot.live`
- Display animated goodbye message for colleagues ([master-atul/byemck](https://github.com/master-atul/byemck)) 
	- `curl byemck.atulr.com`
- Get *Rick Rolled* (also works with telnet) 
	- `nc rya.nc 1987`
- Watch an emoji race ([source](https://glitch.com/edit/#!/node-web-console)) 
	- `curl node-web-console.glitch.me`
- Run Forrest, run!
	- `curl ascii.live/forrest`
- Watch Nyan Cat
	- `curl ascii.live/nyan`
- Fullscreen colorized Nyan Cat 
	- `curl https://poptart.spinda.net`
- Gopher resources / news / weather / entertainment
	- `gopher://fld.gp:70`
- Gopher games, drink recipes, and other
	- `gopher://mozz.us:70`
- 4chan
	- `gopher://port70.net/1board/b`
- BBS (BBS list [here](https://www.telnetbbsguide.com/bbs/)) 
	- `telnet 1984.ws 23`
- Demo the "Monotty" text-based desktop environment ([source](https://github.com/netxs-group/VTM))
	- `ssh vtm@netxs.online`
- Search and display GIFs in your terminal 
	- `curl gif.xyzzy.run`

##### Telnet/SSH Based
- Snake game; play with AWSD keys
	- `ssh sshtron.zachlatta.com`
-  Multiplayer Tetris 
	- `ssh netris.rocketnine.space`
-  2048, snake, and freecell ([source](https://git.causal.agency/play)) 
	- `ssh play@ascii.town`
- 11 arcade games
	- `ssh gameroom@bitreich.org`
- Guess free minesweeper; Pass: play 
	- `ssh play@anonymine-demo.oskog97.com -p 2222`
-  Play various games including checkers 
	- `ssh twenex@sdf.org`
- Competitive puzzle; *password: intricacy*
	- `ssh intricacy@sshgames.thegonz.net`
- Multiplayer Chess; *password: simulchess*
	- `ssh simulchess@sshgames.thegonz.net`
- Pacman; *password: pacman*
	- `ssh pacman:pacman@antimirov.net`
- Roguelike; *password: lag*
	- `ssh lagrogue@sshgames.thegonz.net`
- Khet; *password: ckhet*
	- `ssh ckhet@sshgames.thegonz.net`
- Nethack and others
	- `ssh slashem@slashem.me`
- Rogue; *password: yendor*
	- `ssh rodney@rlgallery.org`
- Singleplayer pong
	- `ssh pong.brk.st`
- Requires you to [make an account](https://sdf.org) first
	- `ssh tty.sdf.org`
- MUD (MUD list [here](http://www.mudconnect.com/cgi-bin/search.cgi?mode=tmc_biglist), also works with telnet) 
	- `nc aardmud.org 23`
- Chess Game (also works with telnet)
	- `nc freechess.org 23`
- Play/watch the game of Go (also works with telnet) 
	- `nc igs.joyjoy.net 6969`
- Multiplayer backgammon (also works with telnet)
	- `nc fibs.com 4321`
- Infinite cave adventure
	- `telnet dungeon.name 20028`
- Games: Pong, Break out, Tetris 
	- `telnet milek7.gq`
- Star Trek 
	- `telnet mtrek.com 1701`
- Multiplayer Star Trek 
	- `telnet decwars.com 1701`
- `telnet telehack.com`
- Multiplayer Zork 
	- `telnet multizork.icculus.org`

## Scripts
Useful scripts, that can be run with just one line of code, but where, still local execution is necessary.
- `curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python -`
- `curl -sL https://raw.githubusercontent.com/dylanaraps/neofetch/master/neofetch | bash`
- `curl -sL https://raw.githubusercontent.com/keroserene/rickrollrc/master/roll.sh | bash`

## Clients
At least one of these clients, that you need to access these services, is installed on almost every UNIX/Linux system.
- [aria2](https://aria2.github.io/)
- [bitsadmin](https://docs.microsoft.com/windows/win32/bits/)
- [curl](https://curl.haxx.se/)
- [httpie](https://httpie.org/)
- [httrack](https://www.httrack.com/)
- [powershell](https://microsoft.com/powershell/)
- [rclone](https://rclone.org/)
- [wget](https://www.gnu.org/software/wget/)
- [wget2](https://gitlab.com/gnuwget/wget2)
