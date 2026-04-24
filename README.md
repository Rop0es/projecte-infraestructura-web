Documentacio del Projecte d'Infraestructura Web
Aquest projecte desplega una arquitectura web escalable
mitjançant Docker, amb un proxy invers i balanceig de
carrega en una xarxa aïllada.

<img width="391" height="559" alt="image" src="https://github.com/user-attachments/assets/e1472984-6b8c-493d-a19c-9ffea149f131" />


Disseny i Decisions Tecniques
Seguretat: Els backends no tenen ports exposats al
host. Només el proxy accepta connexions externes.

Imatges: S'utilitza la imatge oficial de Nginx per
a tota la infraestructura.

Balanceig: S'utilitza Round Robin amb una capçalera
personalitzada (X-Backend-Server) per a la traçabilitat.

Volums: Un "bind-mount" comparteix el contingut de
la carpeta web-content entre els dos servidors.

Guia de Desplegament
Aixecar l'entorn
docker compose up -d

Verificar l'estat
docker compose ps

Verificar el balanceig (PowerShell)
for ($i=1; $i -le 6; $i++) {
$r = Invoke-WebRequest -Uri "http://localhost" -Method Head
$s = $r.Headers["X-Backend-Server"]
Write-Host "Peticio $i: Backend $s"
}

Captures demostració
<img width="856" height="744" alt="image" src="https://github.com/user-attachments/assets/318e9d03-955e-48a1-b4d9-df55a3d6c5c0" />

<img width="1666" height="110" alt="image" src="https://github.com/user-attachments/assets/313c42a0-289b-4d91-bc26-a188a03a41ae" />

<img width="380" height="93" alt="image" src="https://github.com/user-attachments/assets/95a558b3-d2e0-463f-abc1-6c7a473e623f" />

<img width="370" height="90" alt="image" src="https://github.com/user-attachments/assets/79d81cf2-89de-4993-a15e-c57d14af9b50" />
