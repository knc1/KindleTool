# KindleTool
## usage:
* KindleTool md [ &lt;<b>input</b>&gt; ] [ &lt;<b>output</b>&gt; ]

>> Obfuscates data using Amazon's update algorithm.  
>> If no input is provided, input from stdin  
>> If no output is provided, output to stdout  

* KindleTool dm [ &lt;<b>input</b>&gt; ] [ &lt;<b>output</b>&gt; ]

>> Deobfuscates data using Amazon's update algorithm.  
>> If no input is provided, input from stdin  
>> If no output is provided, output to stdout  

* KindleTool convert [<i>options</i>] &lt;<b>input</b>&gt;...

>> Converts a Kindle update package to a gzipped tar archive file, and delete input.

	Options:
		-c, --stdout                Write to standard output, keeping original files unchanged.
		-i, --info                  Just print the package information, no conversion done.
		-s, --sig                   OTA V2 updates only. Extract the payload signature.
		-k, --keep                  Don't delete the input package.
		-u, --unsigned              Assume input is an unsigned & mangled userdata package.
		-w, --unwrap                Just unwrap the package, if it's wrapped in an UpdateSignature header (especially useful for userdata packages).

* KindleTool extract [<i>options</i>] &lt;<b>input</b>&gt; &lt;<b>output</b>&gt;

>> Extracts a Kindle update package to a directory.

	Options:
		-u, --unsigned              Assume input is an unsigned & mangled userdata package.

* KindleTool create &lt;<b>type</b>&gt; &lt;<b>devices</b>&gt; [<i>options</i>] &lt;<b>dir</b>|<b>file</b>&gt;... [ &lt;<b>output</b>&gt; ]

>> Creates a Kindle update package.
>> You should be able to throw a mix of files &amp; directories as input without trouble.  
>> Just keep in mind that by default, if you feed it absolute paths, it will archive absolute paths, which usually isn't what you want!  
>> If input is a single gzipped tarball (".tgz" or ".tar.gz") file, we assume it is properly packaged (bundlefile &amp; sigfile), and will only convert it to an update.
>> Output should be a file with the extension ".bin", if it is not provided, or if it's a single dash, outputs to standard output.
>> In case of OTA updates, all files with the extension ".ffs" or ".sh" will be treated as update scripts.  

	Type:
		ota                         OTA V1 update package. Works on Kindle 3 and older.
		ota2                        OTA V2 signed update package. Works on Kindle 4 and newer.
		recovery                    Recovery package for restoring partitions.
		recovery2                   Recovery V2 package for restoring partitions. Works on Kindle 5 (PaperWhite) and newer
		sig                         Signature envelope. Use this to build a signed userdata package with the -U switch (FW >= 5.1 only, but device agnostic).

	Devices:
		OTA V1 & Recovery packages only support one device. OTA V2 & Recovery V2 packages can support multiple devices.

		-d, --device k1             Kindle 1
		-d, --device k2             Kindle 2 US
		-d, --device k2i            Kindle 2 International
		-d, --device dx             Kindle DX US
		-d, --device dxi            Kindle DX International
		-d, --device dxg            Kindle DX Graphite
		-d, --device k3w            Kindle 3 WiFi
		-d, --device k3g            Kindle 3 WiFi+3G
		-d, --device k3gb           Kindle 3 WiFi+3G Europe
		-d, --device k4             Silver Kindle 4 (No Touch) (2011)
		-d, --device k4b            Black Kindle 4 (No Touch) (2012)
		-d, --device k5w            Kindle 5 (Kindle Touch) WiFi
		-d, --device k5g            Kindle 5 (Kindle Touch) WiFi+3G
		-d, --device k5gb           Kindle 5 (Kindle Touch) WiFi+3G Europe
		-d, --device k5u            Kindle 5 (Kindle Touch) Unknown Variant (4th device code found in Touch official updates).
		-d, --device pw             Kindle PaperWhite WiFi
		-d, --device pwg            Kindle PaperWhite WiFi+3G
		-d, --device pwgc           Kindle PaperWhite WiFi+3G Canada
		-d, --device pwgb           Kindle PaperWhite WiFi+3G Europe
		-d, --device pwgj           Kindle PaperWhite WiFi+3G Japan
		-d, --device pwgbr          Kindle PaperWhite WiFi+3G Brazil
		-d, --device pw2            Kindle PaperWhite 2 (2013) WiFi
		-d, --device pw2j           Kindle PaperWhite 2 (2013) WiFi Japan
		-d, --device pw2g           Kindle PaperWhite 2 (2013) WiFi+3G
		-d, --device pw2gc          Kindle PaperWhite 2 (2013) WiFi+3G Canada
		-d, --device pw2gb          Kindle PaperWhite 2 (2013) WiFi+3G Europe
		-d, --device pw2gr          Kindle PaperWhite 2 (2013) WiFi+3G Russia
		-d, --device pw2gj          Kindle PaperWhite 2 (2013) WiFi+3G Japan
		-d, --device pw2il          Kindle PaperWhite 2 (2013) WiFi (4GB) International
		-d, --device pw2gbl         Kindle PaperWhite 2 (2013) WiFi+3G (4GB) Europe
		-d, --device pw2gl          Kindle PaperWhite 2 (2013) WiFi+3G (4GB)
		-d, --device pw2gcl         Kindle PaperWhite 2 (2013) WiFi+3G (4GB) Canada
		-d, --device pw2gbrl        Kindle PaperWhite 2 (2013) WiFi+3G (4GB) Brazil
		-d, --device kt2            Kindle Basic (2014)
		-d, --device kt2a           Kindle Basic (2014) Australia
		-d, --device kv             Kindle Voyage WiFi
		-d, --device kvg            Kindle Voyage WiFi+3G
		-d, --device kvgb           Kindle Voyage WiFi+3G Europe
		-d, --device kvgj           Kindle Voyage WiFi+3G Japan
		-d, --device kvgm           Kindle Voyage WiFi+3G Mexico
		-d, --device pw3            Kindle PaperWhite 3 (2015) WiFi
		-d, --device pw3g           Kindle PaperWhite 3 (2015) WiFi+3G
		-d, --device pw3gj          Kindle PaperWhite 3 (2015) WiFi+3G Japan
		-d, --device pw3gc          Kindle PaperWhite 3 (2015) WiFi+3G Canada
		-d, --device pw3gb          Kindle PaperWhite 3 (2015) WiFi+3G Europe
		-d, --device pw3gm          Kindle PaperWhite 3 (2015) WiFi+3G Mexico
		-d, --device pw3jl          Kindle PaperWhite 3 (2016) WiFi (32GB) Japan
		-d, --device pw3w           White Kindle PaperWhite 3 (2016) WiFi
		-d, --device pw3wgj         White Kindle PaperWhite 3 (2016) WiFi+3G Japan
		-d, --device pw3wjl         White Kindle PaperWhite 3 (2016) WiFi (32GB) Japan
		-d, --device pw3wgi         White Kindle PaperWhite 3 (2016) WiFi+3G International
		-d, --device pw3wgib        White Kindle PaperWhite 3 (2016) WiFi+3G International (Bis)
		-d, --device koa            Kindle Oasis WiFi
		-d, --device koag           Kindle Oasis WiFi+3G
		-d, --device koagb          Kindle Oasis WiFi+3G Europe
		-d, --device koagbi         Kindle Oasis WiFi+3G International
		-d, --device kt3            Kindle Basic 2 (2016)
		-d, --device kt3w           White Kindle Basic 2 (2016)
		-d, --device kindle2        Alias for k2 & k2i
		-d, --device kindledx       Alias for dx, dxi & dxg
		-d, --device kindle3        Alias for k3w, k3g & k3gb
		-d, --device legacy         Alias for kindle2, kindledx & kindle3
		-d, --device kindle4        Alias for k4 & k4b
		-d, --device touch          Alias for k5w, k5g & k5gb
		-d, --device paperwhite     Alias for pw, pwg, pwgc, pwgb, pwgj & pwgbr
		-d, --device paperwhite2    Alias for pw2, pw2j, pw2g, pw2gc, pw2gb, pw2gr, pw2gj, pw2il, pw2gbl, pw2gl, pw2gcl & pw2gbrl
		-d, --device basic          Alias for kt2 & kt2a
		-d, --device voyage         Alias for kv, kvg, kvgb, kvgj & kvgm
		-d, --device paperwhite3    Alias for pw3, pw3g, pw3gj, pw3gc, pw3gb, pw3gm, pw3jl, pw3w, pw3wgj, pw3wjl, pw3wgi, pw3wgib
		-d, --device oasis          Alias for koa, koag, koagb & koagbi
		-d, --device basic2         Alias for kt3 & kt3w
		-d, --device kindle5        Alias for touch, paperwhite, paperwhite2, basic, voyage, paperwhite3, oasis & basic2
		-d, --device none           No specific device (Recovery V2 & Recovery FB02 with header rev 2 only, default).
		-d, --device auto           The current device (Obviously, has to be run from a Kindle).

	Platforms:
		Recovery V2 & Recovery FB02 with header rev 2 updates only. Use a single platform per package.

		-p, --platform unspecified  Don't target a specific platform.
		-p, --platform mario        Mario (mostly devices shipped on FW 1.x?) [Deprecated].
		-p, --platform luigi        Luigi (mostly devices shipped on FW 2.x?).
		-p, --platform banjo        Banjo (devices shipped on FW 3.x?).
		-p, --platform yoshi        Yoshi (mostly devices shipped on FW <= 5.1).
		-p, --platform yoshime-p    Yoshime (Prototype).
		-p, --platform yoshime      Yoshime (Also known as Yoshime3, mostly devices shipped on FW >= 5.2).
		-p, --platform wario        Wario (mostly devices shipped on FW >= 5.4).
		-p, --platform duet         Duet (mostly devices shipped on FW >= 5.7).
		-p, --platform heisenberg   Heisenberg (mostly devices shipped on FW >= 5.8).

	Boards:
		Recovery V2 & Recovery FB02 with header rev 2 updates only. Use a single board per package.

		-B, --board unspecified     Don't target a specific board, skip the device check.
		-B, --board tequila         Tequila (Kindle 4)
		-B, --board whitney         Whitney (Kindle Touch)

	Options:
		All the following options are optional and advanced.
		-k, --key <file>            PEM file containing RSA private key to sign update. Default is popular jailbreak key.
		-b, --bundle <type>         Manually specify package magic number. May override the value dictated by "type", if it makes sense. Valid bundle versions:
                                      FB01, FB02 = recovery; FB03 = recovery2; FC02, FD03 = ota; FC04, FD04, FL01 = ota2; SP01 = sig
		-s, --srcrev <ulong|uint>   OTA updates only. Source revision. OTA V1 uses uint, OTA V2 uses ulong.
                                      Lowest version of device that package supports. Default is 0.
		-t, --tgtrev <ulong|uint>   OTA & Recovery V2 updates only. Target revision. OTA V1 uses uint, OTA V2 & Recovery V2 uses ulong.
                                      Highest version of device that package supports. Default is ulong/uint max value.
		-h, --hdrrev <uint>         Recovery V2 & Recovery FB02 updates only. Header Revision. Default is 0.
		-1, --magic1 <uint>         Recovery updates only. Magic number 1. Default is 0.
		-2, --magic2 <uint>         Recovery updates only. Magic number 2. Default is 0.
		-m, --minor <uint>          Recovery updates only. Minor number. Default is 0.
		-c, --cert <ushort>         OTA V2 updates only. The number of the certificate to use (found in /etc/uks on device). Default is 0.
                                      0 = pubdevkey01.pem, 1 = pubprodkey01.pem, 2 = pubprodkey02.pem
		-o, --opt <uchar>           OTA V1 updates only. One byte optional data expressed as a number. Default is 0.
		-r, --crit <uchar>          OTA V2 updates only. One byte optional data expressed as a number. Default is 0.
		-x, --meta <str>            OTA V2 updates only. An optional string to add. Multiple "--meta" options supported.
                                      Format of metastring must be: key=value
		-a, --archive               Keep the intermediate archive.
		-u, --unsigned              Build an unsigned & mangled userdata package.
		-U, --userdata              Build an userdata package (can only be used with the sig update type).
		-O, --ota                   Build a versioned OTA bundle (can only be used with the ota2 update type).
		-C, --legacy                Emulate the behaviour of yifanlu's KindleTool regarding directories. By default, we behave like tar:
                                      every path passed on the commandline is stored as-is in the archive. This switch changes that, and store paths
                                      relative to the path passed on the commandline, like if we had chdir'ed into it.


* KindleTool info &lt;<b>serialno</b>&gt;

>> Get the default root password.
>> Unless you changed your password manually, the first password shown will be the right one.  
>> (The Kindle defaults to DES hashed passwords, which are truncated to 8 characters).
>> If you're looking for the recovery MMC export password, that's the second one.  

* KindleTool version

>> Show some info about this KindleTool build.

* KindleTool help

>> Show this help screen.

### notices:
1. If the variable KT_WITH_UNKNOWN_DEVCODES is set in your environment (no matter the value), some device checks will be relaxed with the create command.

2. Kindle 4.0+ has a known bug that prevents some updates with meta-strings to run.
3. Currently, even though OTA V2 supports updates that run on multiple devices, it is not possible to create an update package that will run on both the Kindle 4 (No Touch) and Kindle 5 (Touch/PW).

// kate: indent-mode cstyle; indent-width 4; replace-tabs on; remove-trailing-spaces none;
