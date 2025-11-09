𝒜 (RING & STAR) <br>

<img width="292" height="224" alt="A" src="https://github.com/user-attachments/assets/46cdf0cb-a455-4f83-bcde-c46b150407d5" /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <img width="294" height="246" alt="AA" src="https://github.com/user-attachments/assets/a33df5a3-af1b-439d-8432-7a260eaccce6" /> <br>

(Take 1st Cable)
1)PC0→Desktop→IP Config→IP Address=172.16.0.1  
2)PC1→Desktop→IP Config→IP Address=172.16.0.2 <br> 
3)PC2→Desktop→IP Config→IP Address=172.16.0.3 <br> 
4)PC3→Desktop→IP Config→IP Address=172.16.0.4 <br> 

#####################################################################################<br>

𝕭 (Mesh & BUS) <br>

<img width="298" height="222" alt="B" src="https://github.com/user-attachments/assets/8d672833-4e0c-487c-8944-f9d084324a35" />   <img width="557" height="160" alt="BB" src="https://github.com/user-attachments/assets/e12c5689-26a1-4057-9d6d-b05d9c2ce5fe" />
 <br>

(pc)Fast Ethernet 0 → (switch)Fast Ethernet 0/1 {same All} <br>
then Connect switches <br>
(pc to switch 3rd cable ) (switch to switch 4th cable) <br>
Then config PCs as 𝒜 <br>
to send message (PC→Desktop→Command prompt→Ping 192.168.0.5)

#####################################################################################<br>

𝓒 (layer 2 Switch ) <br>

<img width="476" height="213" alt="C" src="https://github.com/user-attachments/assets/1b6519a3-06cd-42d9-95c6-4a61be6cac5b" /> <br>
Connect pc(FE0) to switch(FE0/1) with 3rd cable (connect for all pcs same) <br>

Connect Switch(gb 0/1) to router(gb 0/0) <br>
PCs→Config → Gateway:192.168.1.254 (Default for all pcs) <br>
then click (AT INTERFACE) fastEthernet0→ Ip Addtess:192.168.1.1 (change ip for every pc) <br>
Router→Config→Interface:gigabit Ethernet 0/0 (same for 0/1) → port Status=ON → IP Address =(Default Gateway) <br>
to send message use cmd prompt → Ping (IP Address) <br>

#####################################################################################<br>

𝕯 (WAN) <br>

<img width="281" height="205" alt="D" src="https://github.com/user-attachments/assets/22e72c28-4600-497c-b087-4765ea1f7422" />


#####################################################################################<br>

𝓔 (TCP)<br>

a. Say Hello to Each other
````````````````````````````````````
import socket
import threading
import time

HOST = '127.0.0.1'  # localhost
PORT = 5001

def server():
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.bind((HOST, PORT))
        s.listen()
        print("[Server] Listening for connections...")
        conn, addr = s.accept()
        with conn:
            print(f"[Server] Connected by {addr}")
            client_msg = conn.recv(1024).decode()
            print(f"[Server] Client says: {client_msg}")
            conn.sendall("Hello from Server!".encode())

def client():
    time.sleep(1)  # Wait for server to start
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((HOST, PORT))
        print("[Client] Connected to server")
        s.sendall("Hello from Client!".encode())
        server_msg = s.recv(1024).decode()
        print(f"[Client] Server says: {server_msg}")

# Run the server in a separate thread
server_thread = threading.Thread(target=server)
server_thread.start()

# Run client on main thread
client()

server_thread.join()
print("Done.")


```````````````````````````````````````````

b.File transfer 

```````````````
import socket
import threading
import time
import os
HOST = '127.0.0.1' # localhost
PORT = 5002
BUFFER_SIZE = 4096
FILE_TO_SEND = "file_to_send.txt"
RECEIVED_FILE = "received_file.txt"
def server():
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.bind((HOST, PORT))
        s.listen()
        print("[Server] Listening for incoming connections...")
        conn, addr = s.accept()
        with conn:
            print(f"[Server] Connected by {addr}")
            with open(RECEIVED_FILE, 'wb') as f:
                while True:
                    data = conn.recv(BUFFER_SIZE)
                    if not data:
                        break
                    f.write(data)
            print(f"[Server] File received and saved as'{RECEIVED_FILE}'.")
def client():
    time.sleep(1) # Wait for server to start
    # Create sample file if not exists
    if not os.path.exists(FILE_TO_SEND):
        with open(FILE_TO_SEND, 'w') as f:
            f.write("This is a sample file sent from the client.\n" * 10)
    with socket.socket(socket.AF_INET,socket.SOCK_STREAM) as s:
        s.connect((HOST, PORT))
        print("[Client] Connected to server")
        with open(FILE_TO_SEND, 'rb') as f:
            while True:
                bytes_read = f.read(BUFFER_SIZE)
                if not bytes_read:
                    break
                s.sendall(bytes_read)
        print(f"[Client] File '{FILE_TO_SEND}' sent successfully.")
# Run server and client using threads
server_thread = threading.Thread(target=server)
server_thread.start()
client()
server_thread.join()
print("File transfer complete.")
`````````````````````````````

#####################################################################################<br>

𝓕 (HTTP,HTTPS,FTP) <br>

<img width="139" height="175" alt="F" src="https://github.com/user-attachments/assets/e2e8cb2c-5ea7-471c-977d-5ff22b58af47" /> <br>
Connect pcs to switch and server through 1st cable <br>
Server→Desktop→IP Config→IPV4 Address=10.10.10.0 <br>
pc1→Desktop→IP Config→IPV4 Address=10.10.10.1 <br>
pc2→Desktop→IP Config→IPV4 Address=10.10.10.2 <br>
then Server→Services(Off other services)→FTP(set username & Pass ,click add)br>
pc→Desktop→cmd prompt→ FTP 10.10.10.0 (then enter userid and pass)(dir,help,put) <br>

#####################################################################################<br>

𝓖 (SSL) <br>

<img width="476" height="221" alt="G" src="https://github.com/user-attachments/assets/23f86f85-409f-4a9f-933a-316400e1afe9" />  <img width="558" height="318" alt="GG" src="https://github.com/user-attachments/assets/7fb1b607-cc89-4cfa-aab5-adcc968dae28" />

Cmd prompt → ping www.flipcart.com <br>

wireshark→ ethernet →(search) <b>ip.addr</b>==163.53.76.86

#####################################################################################<br>

𝓗 (IPsec (ESP and AH)) <br>

<img width="504" height="242" alt="H" src="https://github.com/user-attachments/assets/f7f2846e-53b9-4c82-a95b-7540e2155b2f" /> <img width="562" height="319" alt="HH" src="https://github.com/user-attachments/assets/fc75a4e4-70dc-4ca2-85e1-658ed9ac7be1" />

Cmd prompt → ping www.wekipedia.com <br>
wireshark→ ethernet →(search) <b>ip.addr</b>==(ip)

#####################################################################################<br>

𝓘 (DHCP) <br>

<img width="287" height="263" alt="I" src="https://github.com/user-attachments/assets/6d174c3f-f9cd-424c-9fd7-fd639222739e" /> <br>
after connecting 4 devices to switch <br>
Switch→physical→zoom in → power Off → (add 1st two modules to black box) →  Switch on <br>
then connect remaining cables <br>

Server→Desktop→IP Config → Ipv4 Address=10.0.0.1 <br>
Server→Services→ DHCP→ Default Gateway =10.0.0.1 → Save → ON services(at top) <br>

check
pc→Desktop→IP Config →(click on DHCP) (do same for all devices) <br>

to send message feom pc1 to pc2 <br>
click pc2 → cmd prompt → ping 10.0.0.2 <br>

#####################################################################################<br>

𝓙 (DNS) <br>

`````````````
import socket
def dns_lookup():
  """
  Performs DNS lookups, converting IP to hostname and vice-versa.
  """
  while True:
    print("\nDNS Lookup Tool")
    print("1. IP Address to Hostname")
    print("2. Hostname to IP Address")
    print("3. Exit")
    choice = input("Enter your choice (1, 2, or 3):")
    if choice == '1':
      ip_address = input("Enter the IP address:")
      try:
        hostname = socket.gethostbyaddr(ip_address)[0]
        print(f"Hostname for {ip_address}: {hostname}")
      except socket.herror:
        print(f"Could not find hostname for IP address: {ip_address}")
      except Exception as e:
        print(f"An error occurred: {e}")
    elif choice == '2':
      hostname = input("Enter the hostname:")
      try:
        ip_address = socket.gethostbyname(hostname)
        print(f"IP address for {hostname}: {ip_address}")
      except socket.gaierror:
        print(f"Could not find IP address for hostname: {hostname}")
      except Exception as e:
        print(f"An error occurred: {e}")
    elif choice == '3':
      print("Exiting DNS Lookup Tool.")
      break
    else:
      print("Invalid choice. Please enter 1, 2, or 3.")

if __name__ == "__main__":
  dns_lookup()
``````````````````````````````````````
