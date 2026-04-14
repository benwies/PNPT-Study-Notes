
go install github.com/tomnomnom/assetfinder@latest
assetfinder tesla.com >> tesla-subs.txt
cat tesla-subs.txt | wc -l


assetfinder --subs-only tesla.com

--------------------

https://github.com/owasp-amass/amass

amass enum -d tesla.com

-----------------------

https://github.com/tomnomnom/httprobe

cat final.txt | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443'

------------------------------


Automate with script:

gedit run.sh
#!/bin/bash
$url=$1

if [ ! -d "$url" ];then
		mkdir $url
fi

if [ ! -d "$url/recon" ];then
		mkdir $url/recon
fi

echo "[+] Harvesting subdomains with assetfinder..."
assetfinder $url >> $url/recon/assets.txt
cat $url/recon/assets.text | grep $l >> $url/recon/final.txt
rm $url/recon/assets.txt

echo "[+] Harvesting subdomains with Amass..."
amass enum -d $url >> $url/recon/f.txt
sort -u $url/recon/f.txt >> $url/recon/final.txt
rm $url/recon/f.txt

echo "[+] Probing for alive domains..."
cat $url/recon/final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> $url/recon/alive.txt
