𝒜 (RING & STAR) <br>
<img width="292" height="224" alt="A" src="https://github.com/user-attachments/assets/46cdf0cb-a455-4f83-bcde-c46b150407d5" /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <img width="294" height="246" alt="AA" src="https://github.com/user-attachments/assets/a33df5a3-af1b-439d-8432-7a260eaccce6" /> <br>

(Take 1st Cable)
1)PC0→Desktop→IP Config→IP Address=172.16.0.1  
2)PC1→Desktop→IP Config→IP Address=172.16.0.2 <br> 
3)PC2→Desktop→IP Config→IP Address=172.16.0.3 <br> 
4)PC3→Desktop→IP Config→IP Address=172.16.0.4 <br> 

###########################################################################################################<br>

𝕭 (Mesh & BUS) <br>

<img width="298" height="222" alt="B" src="https://github.com/user-attachments/assets/8d672833-4e0c-487c-8944-f9d084324a35" />  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; <img width="557" height="160" alt="BB" src="https://github.com/user-attachments/assets/e12c5689-26a1-4057-9d6d-b05d9c2ce5fe" />
 <br>

(pc)Fast Ethernet 0 → (switch)Fast Ethernet 0/1 {same All} <br>
then Connect switches <br>
(pc to switch 3rd cable ) (switch to switch 4th cable) <br>
Then config PCs as 𝒜 <br>
to send message (PC→Desktop→Command prompt→Ping 192.168.0.5)

###########################################################################################################<br>

𝓒 <br>
<img width="476" height="213" alt="C" src="https://github.com/user-attachments/assets/1b6519a3-06cd-42d9-95c6-4a61be6cac5b" /> <br>
Connect pc(FE0) to switch(FE0/1) with 3rd cable <br>
Connect Switch(gb 0/1) to router(gb 0/0) <br>
PCs→Config → Gateway:192.168.1.254 (Default for all pcs) <br>
then click (AT INTERFACE) fastEthernet0→ Ip Addtess:192.168.1.1 (change ip for every pc) <br>
Router→Config→Interface:gigabit Ethernet 0/0 (same for 0/1) → port Status=ON → IP Address =(Default Gateway) <br>

