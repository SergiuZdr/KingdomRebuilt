 KingdomRebuilt

Joc de strategie pe ture cu gestiunea unei cetăți și luptă tactică, dezvoltat în Godot 4 (GDScript). Acest document descrie livrabilele proiectului de licență: locația codului sursă, cerințele, pașii de compilare și pașii de instalare/lansare a aplicației.

1. Livrabile

Depozitul conține întregul cod sursă al aplicației: scene și scripturi Godot (`scenes/`, `scripts/`), resurse de date (`data/`), active grafice și audio (`assets/`), configurația proiectului (`project.godot`).

Depozitul nu conține fișiere binare compilate: nu include editorul Godot, build-uri exportate (`.exe`, `.app`, `.pck`) și nici cache-ul intern de import al editorului (`.godot/`). Acestea se generează local, conform pașilor de mai jos.

2. Adresa repository-ului

GitLab UPT: `https://gitlab.upt.ro/sergiu.zdragon/kingdomrebuilt`

Repository-ul este privat, partajat intern. Accesul se acordă la cerere coordonatorului și membrilor comisiei de evaluare (Settings → Members → Invite member, cu rol *Reporter* sau *Developer*), pentru perioada necesară evaluării.

3. Cerințe

- Godot Engine 4.6.x (proiectul folosește rendererul „GL Compatibility”), descărcabil gratuit de la [godotengine.org/download](https://godotengine.org/download). Nu necesită instalare, este un singur executabil portabil.
- Sistem de operare: Windows, Linux sau macOS .

4. Instalare

1. Descărcați și instalați Godot Engine 4.6.x (versiunea standard, nu .NET/C#) pentru sistemul dumneavoastră de operare.
2. Clonați repository-ul:
   ```
   git clone <adresa repository-ului de la secțiunea 2>
   cd KingdomRebuilt
   ```
5. Compilare

GDScript este interpretat, deci nu necesită un pas de compilare separat, dar proiectul trebuie importat o singură dată de motor înainte de prima rulare. Din editor deschideți Godot, alegeți „Import”, navigați la folderul proiectului și selectați `project.godot`. La prima deschidere, editorul importă automat toate resursele.

6. Lansare

Din editor deschideți proiectul în Godot și apăsați `F5` (sau butonul „Play” din colțul din dreapta sus). Scena principală pornește automat.


## 8. Structura codului sursă

| Folder | Conținut |
|---|---|
| `scenes/` | Scene Godot (`.tscn`) pentru UI, luptă, hartă de dungeon |
| `scripts/` | Logica jocului (autoload-uri, date, sisteme de management, luptă, UI) |
| `data/` | Resurse de date (`.tres`) pentru clădiri, unități, abilități |
| `assets/` | Grafică, animații și audio |
| `project.godot` | Configurația proiectului Godot |
