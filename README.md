# Writeup
# Nmap-Port-Scans

## Objective

In this lab I put Nmap through its paces—running stealthy and custom TCP scans, experimenting with packet flags, spoofing and decoying source addresses, fragmenting packets, and even using a zombie host for an idle scan—to uncover how different scan types interact with firewalls and host-based filtering. By comparing results across FIN, NULL, Xmas, Maimon, Window, ACK, SYN, fragmented, spoofed, decoyed, idle, and “reason” scans, I honed my ability to evade simple defenses and accurately enumerate open or unfiltered ports on a target VM.

### Skills Learned

Stealth Scan Variants

FIN (-sF): learned that unfiltered ports show as “open|filtered.”

NULL (-sN) and Xmas (-sX): saw how setting 0 flags vs. all flags affects responses.

Maimon (-sM): observed its unique flag pattern and response behavior.

TCP Window Scan (-sW): counted how many flags remain set in the TCP header.

Custom Flags (--scanflags): manually set the RST flag to craft bespoke probes.

ACK Scan (-sA): distinguished filtered vs. unfiltered ports and detected newly opened ports (e.g. 443).

Source Spoofing & Decoys

-S 10.10.10.11 to fake the source IP.

-D 10.10.20.21,10.10.20.28,ME to insert decoy addresses alongside my own.

Packet Fragmentation (-f / -ff): split TCP segments to slip past simple packet-inspection firewalls.

Idle (Zombie) Scan (-sI): leveraged a third-party host (10.10.5.5) to scan anonymously.

Reason Scan (--reason): used SYN scan (-sS -F --reason) to report why ports were classified (e.g. “syn-ack”).

Comparative Analysis: catalogued flag counts (NULL 0, FIN 1, Xmas 3, Maimon 2, Window 1) and open|filtered port tallies (9 on FIN/null).

### Tools Used

Nmap (v7.80) with flags: -sF, -sN, -sX, -sM, -sW, --scanflags RST, -sA, -S, -D, -f/-ff, -sI, --reason

TryHackMe AttackBox — Linux VM for issuing scans

Terminal (bash) — executing and logging scan output

VPC/Cloud VM — the target instance under test

Wireshark/tcpdump (optional) — to verify packet payloads and fragmentation (if desired)

## Steps
---
Ref.1: Questions
<img width="908" alt="1- questions" src="https://github.com/user-attachments/assets/74595a21-add8-47cf-bb23-ce4cb8f49684" />
---
Ref.2: Null=0, Fin=1, Xmas=3
<img width="724" alt="2- nulll=0,fin=1,xmas=3" src="https://github.com/user-attachments/assets/fac7fe40-2c16-4f8a-98a1-9ad4af87252b" />
---
Ref.3: ran fin scan showed 9 open ports
<img width="537" alt="3- ran fin scan showed 9 open ports" src="https://github.com/user-attachments/assets/ca927600-8649-4f7f-87cf-cfd7f221d164" />
---
Ref.4: Ran null scan showed 9 open ports
<img width="521" alt="4- ran null scan showed 9 open ports" src="https://github.com/user-attachments/assets/d76886ee-ad58-4a35-ad14-2d8548d0a7ba" />
---
Ref.5: Answers
<img width="347" alt="5- answrs" src="https://github.com/user-attachments/assets/637e3369-958c-41fa-a1eb-ac72654b4130" />
---
Ref.6: In the maimon scan 2 flags are set
<img width="726" alt="6- in the maimon scan 2 flags are set" src="https://github.com/user-attachments/assets/25cbc04b-8210-480b-9a35-f7318af1615f" />
---
Ref.7: Questions
<img width="731" alt="7- questions" src="https://github.com/user-attachments/assets/0c6f771b-65f6-4317-92d0-27ed4e7bc0d2" />
---
Ref.8: Answers 1&2 are straightforward
<img width="721" alt="8- answers 1 2, straightforward" src="https://github.com/user-attachments/assets/4ed9d66f-2f2a-49fe-9034-ec7cf4d6252d" />
---
Ref.9: Running ack scan
<img width="560" alt="9- running ack scan" src="https://github.com/user-attachments/assets/96da6d00-5dce-4516-835b-063447dc7e6f" />
---
Ref.10 Answers based on scan results
<img width="326" alt="10- answers based on scsan results" src="https://github.com/user-attachments/assets/26df6dda-f8e5-4ed1-bd10-211021bc4c4a" />
---
Ref.11: answers -s spooding -d decoy ME
<img width="792" alt="11- answers -s spoofing -d decoy me" src="https://github.com/user-attachments/assets/65e9bcf3-3682-4cdb-8ba7-24e221fe9d68" />
---
Ref.12: Spoofing questions
<img width="745" alt="11- spoofing questions" src="https://github.com/user-attachments/assets/4392ebab-92e7-41fb-8ac0-801729c3280f" />
---
Ref.13: ff equals 16 and 64 divided 16 equals
<img width="734" alt="13= -ff equals 16 and 64 divided 16 equals " src="https://github.com/user-attachments/assets/46e9e8bb-dcfc-4221-826a-7ee17b50b919" />
---
Ref.14: Idle scans
<img width="783" alt="14- idle scans" src="https://github.com/user-attachments/assets/8b2c518d-5c38-429e-a9d3-385f642fe692" />
---
Ref.15: Question about reason
<img width="558" alt="15- question about reason" src="https://github.com/user-attachments/assets/ffa1704c-caea-42b6-b303-04b0f62d6572" />
---
Ref.16: Running reason scan
<img width="477" alt="16- running reason scan" src="https://github.com/user-attachments/assets/1d46ee03-f3f0-4ea8-8890-8798aff9397f" />
---
Ref.17: syn ack is answer
<img width="575" alt="17- syn ack is answer" src="https://github.com/user-attachments/assets/2303d6c5-16cb-43d5-9017-934a5b25ab69" />
---
