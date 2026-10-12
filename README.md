# Attribute Xpress

<p align="center">
  <img alt="AppIconHighRes" src="https://github.com/user-attachments/assets/a0e1ce57-fb7a-46a1-a8b6-37c8f39dbda3" width="120" style="border-radius: 12px;" />
</p>

<p align="center">
  <strong>Import and Export Block Attributes with Microsoft Excel for AutoCAD</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AutoCAD-2021--2027-blue.svg" alt="AutoCAD 2021-2027" />
  <img src="https://img.shields.io/badge/Platform-Win64-lightgrey.svg" alt="Platform Win64" />
  <img src="https://img.shields.io/badge/.NET-4.8%20%7C%208.0%20%7C%2010.0-purple.svg" alt=".NET Multi-Target" />
  <img src="https://img.shields.io/badge/Autodesk-App%20Store-E51050.svg" alt="Autodesk App Store" />
</p>

<br>

## ATTXPRESS (Command)
The Attribute Xpress Add-In is an AutoCAD productivity tool designed to streamline reading, exporting, editing, and synchronizing block attributes with Microsoft Excel.

* Live attribute inspection across all attributed block references in an interactive, searchable table.
* Flexible selection modes: pick specific blocks graphically or scan the entire drawing database (Model Space and Layouts).
* Fast two-way CSV export/import for batch editing in Microsoft Excel, Google Sheets, or text editors.
* Side-by-side visual difference preview comparing incoming spreadsheet values against live drawing entities.
* Safe handle-based matching (`Handle`) preventing accidental cross-talk between identically named blocks.
* Demand-loaded architecture ensuring zero performance or startup impact on AutoCAD.
* Full compatibility with vanilla AutoCAD (2021–2027) and AutoCAD Electrical (2021–2027).

<br>

<p align="center">
  <img width="85%" alt="Screenshot 4 - Application Preview" src="https://github.com/user-attachments/assets/d821d692-da72-4d2b-8f4e-bcb63a1ded58" />
</p>

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Download & Installation

### Method 1: Autodesk App Store (Recommended)
1. Download the official installer from the [Autodesk App Store](https://apps.autodesk.com/).
2. Run the MSI installer (automatically configures all installed AutoCAD versions from 2021 through 2027).
3. Launch AutoCAD.
4. Click the **Att Xpress** button on the Ribbon under the **Add-ins** tab, or type **`ATTXPRESS`** at the command prompt.

### Method 2: Autoloader Bundle Deployment
1. Download the latest `AttributeXpress.bundle.zip` release from the Releases tab on the right side of this GitHub repository.
2. Extract the `AttributeXpress.bundle` folder into your ApplicationPlugins directory:
   * **Current User:** `%APPDATA%\Autodesk\ApplicationPlugins\`
   * **All Users:** `%ALLUSERSPROFILE%\Autodesk\ApplicationPlugins\`
3. Launch or restart AutoCAD.
4. When prompted by AutoCAD's security banner on first run, select **Always Load**.
5. At the command prompt, type **`ATTXPRESS`** or click the button in the **Add-ins** ribbon tab.

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Workflow
The application is designed around an intuitive configuration, external spreadsheet editing, and diff-verified synchronization workflow.

### Step 1: Inspect & Select Blocks
Type **`ATTXPRESS`** to open the interface. Click **Select Blocks** to graphically pick specific block references from the canvas, or click **Select All Blocks** to scan all attributed blocks across the entire drawing. Filter results dynamically using the block dropdown or search bar.

<p align="center">
  <img width="80%" alt="Screenshot 1 - Export Attributes" src="https://github.com/user-attachments/assets/cfb911dd-e680-401f-b03c-5b079dfbb204" />
</p>

### Step 2: Export to CSV
Click **Export to CSV** and select your target file path. Attribute Xpress writes each attribute instance with its block name, entity handle, tag name, and current text value into a standard 4-column CSV file.

### Step 3: Edit Data in Excel
Open the exported CSV file in Microsoft Excel or any spreadsheet tool. Modify the entries under the `Value` column as required, then save the file.

<p align="center">
   <img width="80%" alt="Screenshot 3 - Excel Spreadsheet Preview" src="https://github.com/user-attachments/assets/e4e5ecd5-faea-454f-bb34-d27622bd1177" />
</p>

### Step 4: Compare Differences in Import Attributes
Switch to the **Import Attributes** tab inside Attribute Xpress and click **Browse CSV...** to load your updated spreadsheet. The built-in comparison engine instantly compares every row against the active AutoCAD database.

<p align="center">
  <img width="80%" alt="Screenshot 2 - Import Attributes" src="https://github.com/user-attachments/assets/a4b5986f-1818-4bc7-a1b2-7d80690fddcf" />
</p>

### Step 5: Review & Apply to Drawing
Enable the **Modified only** checkbox to isolate rows with changed values. Once verified, click **Apply to Drawing** to commit all updates in an atomic transaction and trigger an automatic drawing regeneration.

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Key Features & Dialog Reference

### Export Attributes Controls
| Setting / Control | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| **Search attributes...** | Text Box | Live filtering across Block Name, Handle, Tag, and Value. | Empty |
| **Filter by block...** | Dropdown | Filters table view to a specific block definition. | `All Blocks` |
| **Block Attributes Table** | DataGrid | Displays Block Name, Handle, Tag, and current Value. | Read-Only Grid |
| **Select Blocks** | Button | Hides dialog to graphically pick block references in AutoCAD. | Interactive |
| **Select All Blocks** | Button | Scans all attributed block references in Model Space and Layouts. | Full Scan |
| **Export to CSV** | Button | Prompts for destination file and exports table data to CSV. | Action |

### Import Attributes Controls
| Setting / Control | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| **Browse CSV...** | Button | Opens a file picker to load an edited CSV file for comparison. | Action |
| **Search attributes...** | Text Box | Live filtering across imported block names, tags, values, and status. | Empty |
| **Filter by block...** | Dropdown | Filters the import comparison preview to a specific block definition. | `All Blocks` |
| **Modified only** | Checkbox | Isolates only rows whose values differ from the drawing database. | `Disabled` |
| **Import Comparison Table** | DataGrid | Displays Block Name, Handle, Tag, Current Value, New Value, and Status. | Comparison Grid |
| **Summary Indicator** | Text Label | Shows real-time count of modified attributes ready to be applied. | Dynamic Count |
| **Apply to Drawing** | Button | Commits all modified values to the AutoCAD database and refreshes view. | Action |

### Comparison Status Indicators
| Status Badge | Meaning | Action Taken on Apply |
| :--- | :--- | :--- |
| `Modified` | The CSV value differs from the drawing's current attribute value. | Updated in drawing database. |
| `Unchanged` | The CSV value exactly matches the current drawing value. | Skipped (no write required). |
| `Block Not Found` | The entity handle in the CSV does not exist in the active drawing. | Skipped with warning. |
| `Tag Not Found` | The block exists, but the specified attribute tag was deleted or renamed. | Skipped with warning. |

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## About this Application
Our goal is to provide the Autodesk community with practical, reliable tools that eliminate repetitive drafting tasks. **Attribute Xpress** was developed to eliminate hours of manual attribute editing by pairing the speed and calculation power of Microsoft Excel with the safety of a visual difference preview inside AutoCAD.

Please report any bugs or suggestions for new functionality by sending a personal message to **@arshdeepsingh404** via your Autodesk Community account. Your feedback is invaluable and will help improve this tool for the entire community.

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Developer
**Arshdeep Singh**<br>
Full-Stack Industrial Automation Developer  
Autodesk Expert Elite | C. Tech | CMSE® | CAPM®

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Version History

| Version | Date | Changes |
| :--- | :--- | :--- |
| **1.0.0** | October 2026 | Initial Release: Dual-tab WPF interface, graphical block selection, drawing-wide scan, CSV export, live search, and visual difference preview synchronization. |

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Compatibility

| AutoCAD Version | Release Series | .NET Runtime Target |
| :--- | :--- | :--- |
| **AutoCAD 2027** | `R26.0` | **.NET 10.0** (`net10.0`) |
| **AutoCAD 2026** | `R25.1` | **.NET 8.0** (`net8.0`) |
| **AutoCAD 2025** | `R25.0` | **.NET 8.0** (`net8.0`) |
| **AutoCAD 2024** | `R24.3` | **.NET Framework 4.8** (`net48`) |
| **AutoCAD 2023** | `R24.2` | **.NET Framework 4.8** (`net48`) |
| **AutoCAD 2022** | `R24.1` | **.NET Framework 4.8** (`net48`) |
| **AutoCAD 2021** | `R24.0` | **.NET Framework 4.8** (`net48`) |

*Also fully compatible with AutoCAD Electrical 2021 through 2027 (`Platform="AutoCAD*|ACADE"`).*

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## Privacy Policy
Attribute Xpress operates entirely offline and locally within AutoCAD. It does not collect, track, transmit, or store any personal information, telemetry, drawing geometry, or metadata. For full details, see [PRIVACY_POLICY.md](PRIVACY_POLICY.md).

&nbsp;
<p align="center">◈ ◈ ◈</p>
&nbsp;

## License
© 2026 Attribute Xpress. All rights reserved.
