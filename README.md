# portscanner

import nmap
import time
from datetime import datetime
import re

ip_add_pattern = re.compile("^(?:[0-9]{1,3}\.){3}[0-9]{1,3}$")

port_range_pattern = re.compile("([0-9]+)-([0-9]+)")

port_min = 0
port_max = 65535

open_ports = []

while True:
    ip_add_entered = input("\33[33;1mInsira o IP que você deseja scanear: ")
    if ip_add_pattern.search(ip_add_entered):
        print(f"{ip_add_entered} é um IP válido!")
        break

while True:

    print("Digite a porta inicial e a final neste padrão: <porta>-<porta> (exemplo 20-80)")
    port_range = input("Digite o range de portas: ")
    port_range_valid = port_range_pattern.search(port_range.replace(" ",""))
    if port_range_valid:
        port_min = int(port_range_valid.group(1))
        port_max = int(port_range_valid.group(2))
        break
    

scanner = nmap.PortScanner()
# We're looping over all of the ports in the specified range.
for port in range(port_min, port_max + 1):
    try:

        result = scanner.scan(ip_add_entered, str(port))
      
        port_status = (result['scan'][ip_add_entered]['tcp'][port]['state'])
        print(f"Port {port} is {port_status}")
    except:

        print(f"Cannot scan port {port}.")
        
        
  #Código executado no sistema operacional windows
        
