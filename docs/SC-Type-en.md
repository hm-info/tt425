# SC type job file information

[Türkçe](SC-Type-tr.md)

This section adds the SC type cutting/job file reference to the TT425 manual. Field definitions come from the **Descriptions** sheet of `TT426 SC type cut file description -en.xlsx`; example records come from `TT426_SCType_Sample.CSV`. The TT426 naming in the source files is preserved.

An illustrative example with fictitious customer, production, profile and file path values is provided instead of the original CSV.

> **Note:** This SC type job file can be used by machines with the HMS_W interface. The CSV does not need to contain all fields listed below. Keep the fields required for file recognition and cutting (`id`, `ksn`, `ksnbar`, `code`, `ktnbar`, `l`, `r`), together with any fields used by the application or the selected FastReport label/barcode template. Fields used only for printing are optional when the template does not use them. HMS_W does not read `nccode`, `isfix` or `subcust`; these columns can be omitted entirely. Macros are not supported.
>
> `DATA1` is not always label-only: when it contains a numeric value, HMS_W also uses it as the profile height. Retain it if the machine's workflow needs that value.

## File structure

The full reference sample uses a semicolon (`;`) as the field separator and contains 29 field names in its first row; each following row describes one part. This is an example, not a requirement to include 29 columns. HMS_W reads SC fields by header name, so the column order may change. Keep the header names and align each record with its header. If a column is omitted, remove both its header and the corresponding value from every record. If a column is retained with an empty value, preserve its separator. The full sample header is:

```text
id;ksn;ksnbar;ktn;ktnbar;l;r;code;info;width;height;trolley;box;orientation;reinf;reinfbar;pos;prono;offno;customer;date;nccode;isfix;colorcode;colorinfo;mainprofile;subcust;image;DATA1
```

[Download the illustrative CSV](downloads/SCType_Example.csv)

## Field definitions

**Yes** in the Cutting and Label columns reproduces the source markings. **—** means no marking/definition is provided; required fields are identified separately in the **Required for HMS_W** column. In that column, **Yes** marks a core field that must be present in the CSV; **No** marks a field included only when needed by the application or FastReport label/barcode template; **Conditional** marks a field needed by the machine's workflow. Retain `DATA1` when a numeric profile height is used. HMS_W does not read `nccode`, `isfix` or `subcust`, so these columns can be omitted. `String(255)` is text, `Integer` is an integer and `Double` is a decimal number. The `l` and `r` fields combine two numbers with `|`.

| Field | Type | Required for HMS_W | Cutting | Label | Description |
| --- | --- | --- | --- | --- | --- |
| `id` | String(255) | Yes | — | Yes | Part id |
| `ksn` | Integer | Yes | — | Yes | Displays the number of the bars installed. As it is shown in sample tab, since the first four lines in the job file are '1', the operations will be done in the same bar. And there are 5 pieces indicated by bar number 2. |
| `ksnbar` | Double | Yes | — | Yes | The bar number(id) is given by ksn. The 59800 number in the work file is 5980.0 mm. The last digit of the 5-digit number indicates the decimal part |
| `ktn` | Integer | No | — | Yes | It refers to the order of parts in the same bar. It is seen that the work file has 4 parts and 1 to 4 values. |
| `ktnbar` | Double | Yes | Yes | Yes | Expresses the length of the part. As it is shown in sample tab, the number entered as 4710 on part1 of bar1 is actually 471.0 mm. (So, the last digit of 4710 indicates the decimal part). |
| `l` | Double &#124; Double | Yes | Yes | Yes | Cutting angle of head of part. The number before "&#124;" character is for the tilt angle. And the number after "&#124;" character for the pivot angle. This values can get decimal value. i.e., 45.55&#124;90.00 |
| `r` | Double &#124; Double | Yes | Yes | Yes | Cutting angle of end of part. The number before "&#124;" character is for the tilt angle. And the number after "&#124;" character for the pivot angle. This values can get decimal value. i.e., 45.55&#124;90.00 |
| `code` | String(255) | Yes | — | Yes | profile code |
| `info` | String(255) | No | — | Yes | Detailed information about bar |
| `width` | Double | No | — | Yes | Frame width |
| `height` | Double | No | — | Yes | Frame height |
| `trolley` | String(255) | No | — | Yes | Indicates that which part will be put in the which trolley |
| `box` | String(255) | No | — | Yes | Indicates that which part will be put in the which box |
| `orientation` | String(255) | No | — | Yes | Location of cut part on the window. (Such as up,down,left)<br>0: Not important<br>1: Meaning Sill or Bottom side<br>2: Meaning Left side<br>3: Meaning Head or Top side<br>4: Meaning Right side Some machining centers using this data |
| `reinf` | String(255) | No | — | Yes | Reinforcement code |
| `reinfbar` | Double | No | — | Yes | Reinforcement length |
| `pos` | String(255) | No | — | Yes | Window no. All parts of window takes the same value. (It is different for each window) |
| `prono` | String(255) | No | — | Yes | Production number |
| `offno` | String(255) | No | — | Yes | Contract number |
| `customer` | String(255) | No | — | Yes | Customer information |
| `date` | String(255) | No | — | Yes | Date |
| `nccode` | String(255) | No | — | — | HMS_W does not read this field and does not support macros. The column can be omitted. |
| `isfix` | — | No | — | — | No type or definition is provided in the source. The sample CSV contains `0`. HMS_W does not read this field; the column can be omitted. |
| `colorcode` | String(255) | No | — | — | Color code descriptions:<br>00: White without gasket<br>01: Bottom colored without gasket<br>02: Top colored without gasket<br>03: Top and bottom colored without gasket<br>10: White with gasket<br>11: Bottom colored with gasket<br>12: Top colored with gasket<br>13: Top and bottom colored with gasket This data used for Haffner four head corner welding and corner cleaner machines |
| `colorinfo` | String(255) | No | — | Yes | color description |
| `mainprofile` | String(255) | No | — | Yes | main profile code Some machining centers using this data |
| `subcust` | — | No | — | — | Detailed customer information. HMS_W does not read this field; the column can be omitted. |
| `image` | String(255) | No | — | Yes | If an image is to be printed to barcode, the path to the image is entered here. |
| `DATA1` | String(255) | Conditional | — | Yes | Optional extra label/barcode information. HMS_W also uses a numeric value as the profile height; retain this field when needed by the machine's workflow. |

## Length and angle notation

The source defines the final digit as the decimal place for `ksnbar` and `ktnbar`:

- `ksnbar = 59800` → 5980.0 mm.
- `ktnbar = 4710` → 471.0 mm.

The source does not separately specify this scaling rule for `width`, `height` or `reinfbar`.

Angles use `tilt|pivot`. The sample contains `l = 45|90` and `r = 135|90`. Decimal angles are supported, for example `45.55|90.00`.

## Orientation codes (`orientation`)

| Code | Location |
| --- | --- |
| 0 | Not important |
| 1 | Sill / Bottom |
| 2 | Left |
| 3 | Head / Top |
| 4 | Right |

The sample CSV contains text with the code, such as `HEAD (3)`, `RIGHT (4)` and `SILL (1)`.

## Color codes (`colorcode`)

| Code | Description |
| --- | --- |
| `00` | White without gasket |
| `01` | Bottom colored without gasket |
| `02` | Top colored without gasket |
| `03` | Top and bottom colored without gasket |
| `10` | White with gasket |
| `11` | Bottom colored with gasket |
| `12` | Top colored with gasket |
| `13` | Top and bottom colored with gasket |

These codes are used by Haffner four head corner welding and corner cleaner machines. `colorinfo` is a separate color description field.

## Macro/NC operation field (`nccode`)

Machines with the HMS_W interface do not support macros and do not read `nccode`. The column can be removed entirely; it does not have to remain as an empty placeholder. `isfix` and `subcust` can also be removed because HMS_W does not read them. If these columns are retained for compatibility with another system, leave `nccode` empty and keep the separators for any empty values.

## Illustrative part example

```csv
id;ksn;ksnbar;ktn;ktnbar;l;r;code;info;width;height;trolley;box;orientation;reinf;reinfbar;pos;prono;offno;customer;date;nccode;isfix;colorcode;colorinfo;mainprofile;subcust;image;DATA1
1;1;59800;1;4710;45|90;135|90;PROFILE001;DEMO PROFILE;4650;4100;1;1;HEAD (3);REINF001;0;1;DEMO-PR001;DEMO-CT001;DEMO CUSTOMER;2026-01-01;;0;10;WHITE WITH GASKET;MAIN001;;images/part-001.wmf;
```

This record describes part 1 of bar 1: bar length 5980.0 mm, part length 471.0 mm, profile code `PROFILE001`, orientation `HEAD (3)`, trolley `1` and box `1`. Customer, production, profile and file path values are illustrative. The image path demonstrates the format only.

[Back to the English manual](English.md)
