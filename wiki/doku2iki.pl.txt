#!/usr/bin/perl 
# easy dokuwiki to ikiwiki conversion
# not perfect, but saves some time
# perl doku2mdwn.pl /tmp/dokuwikipage.txt > newpage.mdwn

$filename = $ARGV[0];

    open(INPUT_FILE, $filename)
        or die "Couldn't open $filename!";

    while (<INPUT_FILE>) {
        chomp($_);
        # headers
        s/======/#/g;
        s/=====/##/g;
        s/====/###/g;
        s/===/####/g;
        s/==/#####/g;
        
        s/^\s\s/    /g; #code
        s/^\s\s\s\s\*/  * /g; #lists, works because of code
        s/\[\[(.*)\|(.*)\]\]/\[\[$2|$1\]\]/g; #links
    
        #s/\(\((.*)\)\)/[][]/g; # footnotes hash?
        #italics no?
        #s/\/\/(.*)\/\//1000/g; #italics kills links
        print $_ . "\n";
    }
    close(INPUT_FILE);

