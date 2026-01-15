# PhosFamilyDice - Mod Baldur's Gate 3

Ce mod ajoute deux fonctionnalités principales :
- **PhosDice** : Un set de textures personnalisées pour les dés d20
- **PhosLuckyDice** : Un nouvel item permettant d'obtenir un boost passif de jet de dé (si équipé)

---

## Fonctionnalités

### PhosDice - Textures de Dés Personnalisées

Un set complet de textures pour le dé d20 incluant :
- `d20.DDS` - Texture principale du dé
- `d20_1.DDS` à `d20_20.DDS` - Textures pour chaque face (1-20)
- `d20_faceCover.DDS` - Texture de couverture des faces
- `single_roll.DDS` - Animation de lancer simple
- `double_roll_1.DDS` / `double_roll_2.DDS` - Animations de double lancer

### PhosLuckyDice - Dé Porte-Bonheur

Un objet légendaire avec les caractéristiques suivantes :
- **Rareté** : Légendaire
- **Poids** : 0.5
- **Valeur** : 18000 or
- **Effets** :
  - `+2` aux jets de compétences (SkillCheck)
  - `+1` aux jets d'attaque (Attack)
  - `+1` aux jets de sauvegarde (SavingThrow)



## Structure du Mod

```
PhosFamilyDice/
├── Mods/
│   └── PhosFamilyDice/
│       ├── meta.lsx                    # Métadonnées du mod
│       ├── GUI/
│       │   ├── metadata.lsx            # Métadonnées GUI
│       │   └── Assets/DiceSets/
│       │       └── PhosDice/           # Textures des dés
│       │           ├── d20.DDS
│       │           ├── d20_1.DDS ... d20_20.DDS
│       │           ├── d20_faceCover.DDS
│       │           ├── single_roll.DDS
│       │           └── double_roll_*.DDS
│       └── Localization/
│           ├── English/PhosFamilyDice.xml
│           └── French/PhosFamilyDice.xml
├── Public/
│   ├── Game/GUI/Assets/                # Icônes de l'objet
│   │   ├── ControllerUIIcons/items_png/
│   │   │   └── Item_LOOT_PhosLuckyDice_Icon.DDS
│   │   └── Tooltips/ItemIcons/
│   │       └── Item_LOOT_PhosLuckyDice_Icon.DDS
│   └── PhosFamilyDice/
│       ├── Assets/
│       │   ├── Item_LOOT_PhosLuckyDice_Model.GR2   # Modèle 3D compilé
│       │   ├── Item_LOOT_PhosLuckyDice_Model.xml   # Définition du modèle 3D
│       │   └── Textures/
│       │       ├── Icons/
│       │       │   └── PhosFamilyDice_Icons.dds    # Icône inventaire (atlas)
│       │       └── 3d_maps/
│       │           ├── PhosFamilyDice_bm.DDS       # Texture basecolor
│       │           ├── PhosFamilyDice_nm.DDS       # Texture normalmap
│       │           └── PhosFamilyDice_pm.DDS       # Texture physicalmap
│       ├── Content/
│       │   ├── [PAK]_PhosFamilyDice/
│       │   │   └── _merged.lsx         # MaterialBank + TextureBank (3D) + VisualBank
│       │   └── UI/[PAK]_UI/
│       │       └── _merged.lsx         # TextureBank (icônes)
│       ├── CustomDice/CustomDice.lsx   # Définition du set de dés
│       ├── DLC/DLC.lsx                 # Définition du DLC
│       ├── GUI/Icons_Items.lsx         # TextureAtlas des icônes
│       ├── RootTemplates/merged.lsx    # Template de l'objet
│       └── Stats/Generated/
│           ├── TreasureTable.txt       # Table de loot
│           └── Data/
│               ├── Armor.txt           # Stats de l'objet
│               └── Spell_*.txt         # Stats des sorts (optionnel)
└── summon                              # Script pour invoquer l'objet
```

---

## Import des Textures

### Prérequis

- **LSLib Toolkit** pour la compilation du mod et des fichier `*.lsx`
- **BG3 Modder's Multitool**
- **NVIDIA Texture Tools** ou équivalent pour exporter en DDS

### Textures PhosDice (Set de Dés)

Les textures de dés se trouvent dans :
```
Mods/PhosFamilyDice/GUI/Assets/DiceSets/PhosDice/
```

#### Format des fichiers

| Fichier | Dimension | Description |
|---------|-----------|-------------|
| `d20.DDS` | 512x512 | Texture principale du dé |
| `d20_1.DDS` à `d20_20.DDS` | 128x128 | Texture de chaque face |
| `d20_faceCover.DDS` | 128x128 | Couverture des faces |
| `single_roll.DDS` | 256x256 | Animation lancer simple |
| `double_roll_1/2.DDS` | 256x256 | Animation double lancer |

Il nous faut ensuite ajouter des fichiers de description pour lier les textures du dé au jeu:

- `Public\PhosFamilyDice\CustomDice\CustomDice.lsx`: dans ce fichier on peut décrire le dé avec un nom, une description...
- `Public\PhosFamilyDice\DLC\DLC.lsx`: dans ce fichier on peut définir un nouveau contenu de jeu

### Icône PhosLuckyDice (Item)

L'icône de l'objet se trouve dans trois emplacements :
| Fichier | Dimension | Description |
|---------|-----------|-------------|
| `Public\Game\GUI\Assets\ControllerUIIcons\items_png\Item_LOOT_PhosLuckyDice_Icon.DDS` | 144x144 | Il est vu au même endroit que pour l'item ci-dessous mais est affiché uniquement pour les joueurs mannettes |
| `Public\Game\GUI\Assets\Tooltips\ItemIcons\Item_LOOT_PhosLuckyDice_Icon.DDS` | 380x380 | Icon avec la meilleure qualité - Il est affiché quand on passe la souris sur l'item dans l'inventaire |
| `Public\PhosFamilyDice\Assets\Textures\Icons\PhosFamilyDice_Icons.dds` | 64x64 | Icône de l'objet dans l'inventaire |

> [!warning]
>
> Pour avoir l'icône dans l'inventaire il faut **absolument** crée un 'TextureAtlas' (`Public\PhosFamilyDice\GUI\Icons_Items.lsx`). Les textures atlas sont des fichiers permettant d'importer des tuiles d'assets dans le jeu. 
>
> E.G. j'ai une image de 128x128 contenant 4 photos en 64x64, on peut alors décrire dans le texture atlas ces 4 images pour pouvoir les importer aux endroits appropriés
>
>
> On viendra définir dans `Public\PhosFamilyDice\Content\UI\[PAK]_UI\_merged.lsx` le lien vers l'atlas

> [!tip]
>
> Les fichiers doivent tous avoir le même non au risque de ne pas avoir de texture en jeu

### Modèle 3D PhosLuckyDice

Pour ajouter un modèle 3D personnalisé à l'objet PhosLuckyDice, deux fichiers sont nécessaires :

| Fichier | Description |
|---------|-------------|
| `Public/PhosFamilyDice/Assets/Item_LOOT_PhosLuckyDice_Model.xml` | Définition du modèle 3D (mesh, matériaux, UV mapping) |
| `Public/PhosFamilyDice/Assets/Item_LOOT_PhosLuckyDice_Model.GR2` | Modèle 3D compilé au format GR2 (Granny 3D) |

#### Configuration dans `_merged.lsx`

Le modèle 3D est référencé dans `Public/PhosFamilyDice/Content/UI/[PAK]_UI/_merged.lsx` via la région `VisualBank` :

| Attribut | Valeur | Description |
|----------|--------|-------------|
| `ID` | `bb36583d-e193-4998-97dc-d132ace3da29` | UUID unique du visual |
| `Name` | `Item_LOOT_PhosLuckyDice_Model` | Nom du modèle (sans extension) |
| `SourceFile` | `Public/PhosFamilyDice/Assets/Item_LOOT_PhosLuckyDice_Model.GR2` | Chemin vers le fichier GR2 |
| `Template` | `Public/PhosFamilyDice/Assets/Item_LOOT_PhosLuckyDice_Model.Unnamed.0` | Référence au template du mesh |
| `ObjectID` | `Item_LOOT_PhosLuckyDice_Model.Cube.0` | ID de l'objet mesh dans le modèle |
| `MaterialID` | `9e2966c7-b61c-4bc1-bef1-a79cb5fde067` | UUID du matériau appliqué |

#### Workflow de création du modèle 3D

1. **Créer le modèle** dans Blender ou un autre logiciel 3D
2. **Exporter en GR2** grâce à l'addon blender adéquat
4. **Créer le fichier XML** décrivant le modèle (généré automatiquement par LSLib)
5. **Mettre à jour `_merged.lsx`** avec les bonnes références

### Textures 3D du Modèle

#### Types de textures

Les textures se trouvent dans `Public/PhosFamilyDice/Assets/Textures/3d_maps/` :

| Fichier | Suffixe | Description |
|---------|---------|-------------|
| `PhosFamilyDice_bm.DDS` | `_bm` (basecolor map) | Texture de couleur principale (diffuse/albedo) |
| `PhosFamilyDice_nm.DDS` | `_nm` (normal map) | Carte de normales pour les détails de relief |
| `PhosFamilyDice_pm.DDS` | `_pm` (physical map) | Carte physique (metallic, roughness, AO) |

> [!tip]
> 
> Les textures doivent être exportées au format **DDS** (BC7 ou BC3 recommandé).
> La résolution recommandée est de **4096x4096** pour une qualité optimale ou tout autre puissance de deux.

#### Lier les textures au modèle 3D

Pour lier les textures au modèle 3D, il faut créer une entrée dans le fichier `Public/PhosFamilyDice/Content/[PAK]_PhosFamilyDice/_merged.lsx` avec trois régions :

##### 1. TextureBank - Déclaration des textures

Chaque texture doit être déclarée dans la région `TextureBank` :

```xml
<region id="TextureBank">
    <node id="TextureBank">
        <children>
            <!-- Texture de couleur (basecolor) -->
            <node id="Resource">
                <attribute id="ID" type="FixedString" value="[UUID_UNIQUE]" />
                <attribute id="Name" type="LSString" value="PhosFamilyDiceBody" />
                <attribute id="SRGB" type="bool" value="True" />  <!-- True pour basecolor -->
                <attribute id="SourceFile" type="LSString" value="Public/PhosFamilyDice/Assets/Textures/3d_maps/PhosFamilyDice_bm.DDS" />
                <attribute id="Streaming" type="bool" value="True" />
                <attribute id="Type" type="int32" value="1" />
                <attribute id="Width" type="int32" value="4096" />
                <attribute id="Height" type="int32" value="4096" />
            </node>
            <!-- Répéter pour normalmap (SRGB=False) et physicalmap (SRGB=False) -->
        </children>
    </node>
</region>
```

> [!important]
> 
> - `SRGB` doit être `True` uniquement pour la texture **basecolor**
> - `SRGB` doit être `False` pour les textures **normalmap** et **physicalmap**

##### 2. MaterialBank - Création du matériau

Le matériau lie les textures ensemble et définit les propriétés de rendu :

```xml
<region id="MaterialBank">
    <node id="MaterialBank">
        <children>
            <node id="Resource">
                <attribute id="ID" type="FixedString" value="[UUID_MATERIAU]" />
                <attribute id="MaterialType" type="uint8" value="4" />
                <attribute id="Name" type="LSString" value="PhosFamilyDice_Material" />
                <attribute id="SourceFile" type="LSString" value="Public/Shared/Assets/Materials/Base/Base_AlphaTest.lsf" />
                <children>
                    <!-- Référence vers la texture basecolor -->
                    <node id="Texture2DParameters">
                        <attribute id="Enabled" type="bool" value="True" />
                        <attribute id="ID" type="FixedString" value="[UUID_TEXTURE_BASECOLOR]" />
                        <attribute id="ParameterName" type="FixedString" value="basecolor" />
                    </node>
                    <!-- Référence vers la texture normalmap -->
                    <node id="Texture2DParameters">
                        <attribute id="Enabled" type="bool" value="True" />
                        <attribute id="ID" type="FixedString" value="[UUID_TEXTURE_NORMALMAP]" />
                        <attribute id="ParameterName" type="FixedString" value="normalmap" />
                    </node>
                    <!-- Référence vers la texture physicalmap -->
                    <node id="Texture2DParameters">
                        <attribute id="Enabled" type="bool" value="True" />
                        <attribute id="ID" type="FixedString" value="[UUID_TEXTURE_PHYSICALMAP]" />
                        <attribute id="ParameterName" type="FixedString" value="physicalmap" />
                    </node>
                </children>
            </node>
        </children>
    </node>
</region>
```

##### 3. VisualBank - Liaison avec le modèle 3D

Le matériau est ensuite appliqué au modèle via la région `VisualBank` :

```xml
<region id="VisualBank">
    <node id="VisualBank">
        <children>
            <node id="Resource">
                <attribute id="ID" type="FixedString" value="[UUID_VISUAL]" />
                <attribute id="Name" type="LSString" value="Item_LOOT_PhosLuckyDice_Model" />
                <attribute id="SourceFile" type="LSString" value="Public/PhosFamilyDice/Assets/Item_LOOT_PhosLuckyDice_Model.GR2" />
                <children>
                    <node id="Objects">
                        <attribute id="ObjectID" type="FixedString" value="Item_LOOT_PhosLuckyDice_Model.Cube.0" />
                        <attribute id="MaterialID" type="FixedString" value="[UUID_MATERIAU]" />
                    </node>
                </children>
            </node>
        </children>
    </node>
</region>
```

> [!tip]
> 
> L'`ObjectID` correspond au nom de l'objet mesh dans le fichier GR2.
> Le `MaterialID` doit correspondre à l'UUID du matériau défini dans `MaterialBank`.

#### Workflow complet pour les textures 3D

1. **Créer les textures** dans un logiciel de création (Substance Painter, Photoshop, etc.)
2. **Exporter en DDS** avec les suffixes appropriés (`_bm`, `_nm`, `_pm`)
3. **Placer les fichiers** dans `Public/PhosFamilyDice/Assets/Textures/3d_maps/`
4. **Générer les UUID** pour chaque texture et le matériau via BG3 Modder's Multitool
5. **Créer/Mettre à jour** `[PAK]_PhosFamilyDice/_merged.lsx` avec :
   - Les déclarations des textures dans `TextureBank`
   - La définition du matériau dans `MaterialBank`
   - La liaison dans `VisualBank`
6. **Compiler** le mod avec LSLib Toolkit

---

## Description des Fichiers Clés

> [!tip]
> On peut facilement générer les UUID/H-UUID (UUID pour les traductions) à partir de BG3 Modder's Multitool
>
> ![image-20251207161533775](.assets/README/image-20251207161533775.png)
>
> ![image-20251207161548597](.assets/README/image-20251207161548597.png)

> [!IMPORTANT]
>
> Si la checkbox "handle" est cochée les UUID générées doivent être utilisées pour les traductions

### `Public/PhosFamilyDice/CustomDice/CustomDice.lsx`

Définit le **set de dés personnalisé** :
- **Name** : `PhosDice`
- **UUID** : `a1b2c3d4-e5f6-7890-abcd-ef1234567890`
- **DisplayName** / **Description** : Références vers les textes de localisation

### `Public/PhosFamilyDice/RootTemplates/merged.lsx`

Définit le **template de l'objet PhosLuckyDice** :
- **MapKey** : `308555cb-3b93-4243-b6df-b8cca02d335b`
- **Name** : `PhosLuckyDice`
- **Icon** : `Item_LOOT_PhosLuckyDice_Icon`
- **Stats** : `Item_LOOT_PhosLuckyDice`

### `Public/PhosFamilyDice/Stats/Generated/Data/Armor.txt`

Définit les **statistiques** de l'objet :
```txt
new entry "Item_LOOT_PhosLuckyDice"
type "item"
using "ARM_Ring_Gold"
data "Rarity" "Legendary"
data "Boosts" "RollBonus(SkillCheck, 1);RollBonus(Attack, 1);RollBonus(SavingThrow, 1)"
data "Weight" "0.5"
data "Value" "4000"
```

### `Localization/*/PhosFamilyDice.xml`

Fichiers de **traduction** (Anglais/Français) :
- Nom et description de PhosLuckyDice
- Nom et description de PhosDice



---

## Installation

1. Compilez (se référer au [guide](##Compilation)) le mod via le multitool ou bien téléchargez la release disponible sur github
2. **Placez le fichier** `.pak` dans :

   ```
   %LocalAppData%\Larian Studios\Baldur's Gate 3\Mods
   ```
3. **Activez le mod** dans le gestionnaire de mods ou avec **BG3 Mod Manager**

---

## Compilation

1. Cloner le dépôt

2. Ouvrir Lslib Toolkit

3. Convertir les fichiers de localisation:

   ![image-20251207154723241](.assets/README/image-20251207154723241.png)

4. Compiler les fichier de description comme sur l'image ci-dessous

​	![image-20251207155021838](.assets/README/image-20251207155021838.png)

5. Compiler ensuite le mod avec BG3 MM ou Lslib toolkit

   ![image-20251207155055366](.assets/README/image-20251207155055366.png)

---

## Obtenir l'objet en jeu

### Via la console de debug

Utilisez la commande du fichier `summon` :

```lua
Osi.TemplateAddTo ("308555cb-3b93-4243-b6df-b8cca02d335b", GetHostCharacter (), 1, 1)
```

### Via le loot naturel

L'objet est ajouté à la table de trésor `TUT_Chest_Potions` (coffres du tutoriel).

---

## Notes

> [!note]
>
> Les textures 3D du modèle PhosLuckyDice ont été ajoutées dans `Public/PhosFamilyDice/Assets/Textures/3d_maps/`
>
> Aucune image de mod n'a été intégrée

