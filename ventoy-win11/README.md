# Windows 11 Pro na Ventoy – automatická instalace

## Co nahrát na Ventoy disk (D:)

```
D:\
├── Windows\
│   └── Win11_xxx_Czech_x64.iso        ← ISO z microsoft.com/software-download/windows11
└── ventoy\
    ├── ventoy.json
    └── script\
        └── autounattend.xml
```

1. Stáhni **Windows 11 (multi-edition ISO), čeština, 64bit** z https://www.microsoft.com/software-download/windows11
2. Na D: vytvoř složku `Windows` a ISO dej do ní.
3. Složku `ventoy` z tohoto repozitáře zkopíruj do kořene D:.
4. Doporučeno: aktualizuj Ventoy (Ventoy2Disk.exe → Update) – data zůstanou.

## Instalace na PC

1. Nabootuj z USB (F12 / F11 / F8 / Esc podle výrobce), vyber ISO.
2. Ventoy se zeptá na šablonu → vyber **autounattend.xml**.
3. Jediná ruční věc: **výběr disku** (smaž staré oddíly na cílovém disku a vyber nealokované místo).
4. Zbytek proběhne sám: Windows 11 **Pro**, čeština, česká klávesnice, středoevropský čas,
   místní účet **Uzivatel** (správce, bez hesla), bez účtu Microsoft, bez kontroly TPM/Secure Boot.

## Po instalaci

- **Windows Update** – spusť a opakuj, dokud není vše aktuální.
- Nastav heslo účtu.
- Aktivace: Nastavení → Systém → Aktivace → zadej svůj klíč Windows 11 Pro
  (generický klíč v šabloně systém **neaktivuje**, jen vybere edici Pro).
