# 02 - The Guard: Pi-hole and Network-Wide DNS

Once I had a stable environment with Docker, the goal shifted from infrastructure to utility. I wanted to move beyond just hosting a container to creating something that actively improved my daily digital experience. The most obvious target was the noise of the modern internet. I was tired of browser-based ad blockers that only worked on one device and were easily bypassed by trackers embedded in mobile apps or smart TVs.

The research led me to DNS-level blocking. I realized that instead of trying to hide an ad once it reached my screen, I could stop the request from ever being fulfilled. By turning the Pi into my network’s "phonebook" via Pi-hole, I could tell the system to simply refuse to look up the addresses of known ad and tracking servers. This wasn't just about aesthetics; it was about taking control of the data leaving my house.

Deploying Pi-hole was the first real test of my Docker foundation. It required navigating the specifics of network ports—specifically Port 53, the standard for DNS. I had to learn how to disable the Pi’s internal resolver to clear a path for the container to take over. This was a "eureka" moment in understanding how Linux handles traffic. I used the following configuration to get the guard online:

\`docker run -d --name pihole -p 53:53/tcp -p 53:53/udp -p 80:80 -e TZ="UTC" -v "\$(pwd)/etc-pihole:/etc/pihole" -v "\$(pwd)/etc-dnsmasq.d:/etc/dnsmasq.d" --restart=always pihole/pihole:latest\`

The justification for the effort was immediate. The second I pointed my router’s DNS settings to the Pi, the dashboard came alive. Seeing the "Total Queries Blocked" percentage climb for the first time was the most satisfying moment of the project so far. It validated the entire homelab concept. My network was no longer just a collection of connected devices; it was a filtered, faster, and more private environment.
