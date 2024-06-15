---
description: My General Skills On SIM Cards Analysis
---

# SIM Card Analysis

## Learning Outcomes

* Understand the unique identifiers associated with a SIM card
* Decode SIM Card identifiers from a mobile phone
* Determine when to use a SIM Clone
* Familiarized with Freeware for obtaining data from a SIM card and its use
* Decode timestamps from SIM card messages

## Requirements

all you need is a basic understanding of smartphones and mobile devices. Using a hardware SIM Card reader is highly recommended for testing

## Carrier Networks

{% embed url="https://www.youtube.com/watch?v=TY8egGohOus" %}

Wireless carriers are faced with choosing a radio network standard for which every device on their network must be compatible. The three most popular radio networks used by carriers are Code-Division Multiple Access (CDMA), Global System for Mobile Communication (GSM), and most recently Long-Term Evolution (LTE). LTE utilizes fourth-generation technologies while CDMA and GSM utilize second and third-gen technologies.

<figure><img src="../.gitbook/assets/image (41) (1).png" alt=""><figcaption><p><strong>Mobile Communication Standards</strong></p></figcaption></figure>

Many newer phones often utilize LTE for fast networking and other networks for messaging and calls only. CDMA and GSM networks are constantly shut down as they are being replaced outright by LTE networks. Fifth-generation technologies are greatly influenced by LTE yet make use of a higher frequency radio band to provide even faster speeds.

## Subset Networks&#x20;

Universal Mobile Telecommunications Service (UMTS) networks are a subset of GSM networks. While heavily based on both GSM and CDMA technologies, the network requires specialized hardware. The UMTS network was able to compete with comparative CDMA technologies at the time of its release (2002) and offered speedy telecom interaction speeds.&#x20;

The Enhanced Data rates for GSM Evolution (EDGE) network (released in 2003) cooperated with existing GSM networks to provide faster transmission speeds.



## What are SIM Cards?&#x20;

Subscriber Identity Module (SIM) cards serve as small, sometimes removable, memory units capable of containing keys and information necessary for a phone to reach out to a carrier and fulfill operation. Such cards come in several unique packages and may contain extra features.

{% hint style="info" %}
Wikipedia : [https://en.wikipedia.org/wiki/SIM\_card](https://en.wikipedia.org/wiki/SIM\_card)
{% endhint %}

### Also Recommended Video From Liveoverflow:

{% embed url="https://www.youtube.com/watch?v=iJFnYBJJiuQ" %}

## Smart Cards&#x20;

Smart Cards, as defined by the European Telecommunications Standards Institute, are “microprocessor equipped tokens, able to store and process a diverse range of data and applications” . Such cards range from business-card sized security keys to microscopic integrated circuits. SIM Cards are a form of Smart Card. SIM cards contain a processing module, a file system, and an embedded operating system. Embedded security mechanisms prevent full one-to-one dumps of the device. File system access control lists provide the opportunity to request and receive data.

### Recommended Video From "Mental Outlaw" :&#x20;

{% embed url="https://www.youtube.com/watch?v=bjRcnr_YW8M" %}

## Universal Integrated Circuit Cards(UICCS)&#x20;

Alluding to the physical hardware package, UICCs are the latest generation of SIM smart cards. These cards are a subset of smart cards defined by ETSI as cards that “conform to the specification written and maintained by the ETSI Smart Card Platform project” \[2]. The terms “SIM” and “UICC” are often used interchangeably within the forensics community, however, while UICC refers to a specific generation of SIM cards, SIM and Universal SIM (USIM) denote the application in which cards are utilized.&#x20;

Universal Integrated Circuit Cards are currently used in both GSM and CDMA-compatible devices, along with Integrated Digital Enhanced Network (iDEN) and Blackberry handsets. The introduction to CDMA networks is a newer feature that may not remain true across older devices. The circuit cards may also be used for satellite-connected networks.&#x20;

The generic “SIM” card is compatible with GSM carriers only while CDMA carriers require Removable User Identity Module (R-UIM) or CDMA2000 Subscriber Identity Module (CSIM) cards. These cards provide Similar functionality to the standard GSM-compatible SIM cards. It is possible for a SIM card to support multiple applications.

These cards contain a fully functional embedded system consisting of a microprocessor (CPU), Random Access Memory (RAM), Read-Only Memory (ROM), and Electronically Erasable Programmable ROM (EEPROM). Application Protocol Data Unit (APDU) commands are the standard for communication between devices and smart cards. Technical communication protocol and commands are documented in ETSI TS 102.221 \[2]. UICC and APDU hardware and software are both extensively documented.&#x20;

UICC circuits will terminate to either six or eight contact pads. The layout may vary between UICC applications, however, the terminals’ locations for each required contact will remain the same across all layouts. Each pad is designated for specific input or functionality:

<figure><img src="../.gitbook/assets/image (42) (1).png" alt=""><figcaption><p><strong>SIM Card Pinout</strong></p></figcaption></figure>

VCC is a five-volt-in path to provide power to the integrated circuit. VPP is the programming voltage – this input serves as an electronic interface to program and erase memory. I/O provides input/output to the circuit. Adapters are available to externally power and interact with UICC devices.&#x20;

Note that the pinout remains the same across both 6 and 8 pad circuits. The 6-pad processor contains contact points C1, C2, C3, C5, C6, and C7. Pads C4 and C8 are reserved for auxiliary or USB interfaces. These pads are entirely optional and often foregone as the functionality is not needed. (Used in some other UICC applications, but not used in SIM cards)

Pads may have unique layouts; this will depend on the integrated circuit.&#x20;

{% hint style="info" %}
For a full pinout, guide see:&#x20;

http://pinoutguide.com/Memory/SmartCardIso\_pinout.shtml
{% endhint %}

## Standard SIM Formats and Embedded SIM Cards

## **Overview**

SIM cards (Subscriber Identity Modules) are integral to mobile communication, storing the subscriber's information and enabling connectivity. Over time, SIM card formats have evolved to become smaller and more efficient while maintaining the same core functionalities.

## **Standard SIM Formats**

1. **Full-size SIM (1FF)**
   * **Dimensions**: 85.6 mm x 53.98 mm
   * **Description**: This original SIM card is the size of a standard credit card. The SIM chip on both the credit card and full-size SIM card is the same size, with identical connectors and pad layouts.
   * **Usage**: Rarely used in modern devices but occasionally seen in older models and some specialized equipment.
2. **Mini-SIM (2FF)**
   * **Dimensions**: 25 mm x 15 mm
   * **Description**: Commonly referred to as the "standard" SIM card, the mini-SIM was released in 2004 and quickly became popular in mobile devices.
   * **Usage**: Widely used in older smartphones and other mobile devices until the early 2010s.
3. **Micro-SIM (3FF)**
   * **Dimensions**: 15 mm x 12 mm
   * **Description**: Smaller than the mini-SIM, the micro-SIM was introduced with smartphones like the iPhone 4.
   * **Usage**: Common in smartphones and tablets during the early 2010s.
4. **Nano-SIM (4FF)**
   * **Dimensions**: 12.3 mm x 8.8 mm
   * **Description**: The smallest form factor of traditional SIM cards, introduced with devices such as the iPhone 5.
   * **Usage**: Standard in most modern smartphones and tablets from 2012 onward.

## **Embedded SIM Cards (eSIM)**

**eSIM** (embedded SIM) technology integrates the SIM functionality directly into a device’s hardware, offering numerous advantages over traditional removable SIM cards.

* **Form Factor**: MFF2 (Machine-to-Machine Form Factor)
  * **Dimensions**: 6 mm x 5 mm x ≤ 1 mm
  * **Description**: Embedded directly into the device’s motherboard, making it more compact and resilient to physical damage.
* **Advantages**:
  * **Space-saving**: Frees up space inside devices for other components or a larger battery.
  * **Durability**: Less prone to physical damage as it is non-removable.
  * **Convenience**: Allows users to switch carriers and manage multiple carrier profiles without needing a physical SIM card. This feature is particularly useful for devices like smartphones, smartwatches, and IoT devices.
  * **Security**: Harder to tamper with compared to removable SIM cards.
* **Applications**:
  * **IoT Devices**: Connected cars, GPS systems, smart meters, and other IoT devices benefit from the compact and durable nature of eSIMs.
  * **Consumer Electronics**: Devices such as the Apple Watch, the 2nd generation iPad and later, and Google Pixel phones with Project Fi support eSIM technology.
  * **Smartphones**: Many high-end smartphones, including newer models from Apple and Google, support eSIMs alongside traditional SIM cards.

## **Integrated SIM (iSIM)**

**iSIM** (integrated SIM) represents the next step in SIM card evolution, integrating SIM capabilities directly into a device’s main processor.

* **Advantages**:
  * **Size Reduction**: By embedding the SIM directly into the processor, devices can be made even smaller, which is ideal for compact IoT applications.
  * **Efficiency**: Reduces the need for a separate SIM card component, potentially lowering production costs and power consumption.
* **Applications**: Primarily used in small IoT devices where space and power efficiency are critical.

### **Usage and Compatibility**

* **Adapters**: Many modern devices come with SIM card trays that support multiple SIM formats (Nano-SIM, Micro-SIM, and sometimes Mini-SIM) using adapters.
* **eSIM Adoption**: Increasingly common in newer smartphones, wearables, and IoT devices due to their advantages in size, convenience, and security.
* **iSIM Adoption**: Expected to grow in prevalence as more devices, particularly those in the IoT space, adopt this technology for its space and power-saving benefits.



<figure><img src="../.gitbook/assets/image (44) (1).png" alt=""><figcaption><p>SIM Card and CC card Size Comparison </p></figcaption></figure>

## SIM Applications

**Overview**

SIM applications are essential software bridges that facilitate interaction between SIM card hardware and the devices they are installed in. Different networks require specialized SIM applications to ensure proper communication and functionality. These applications must support various SIM card protocols to be compatible with different network types and devices.

### **Types of SIM Applications**

1. **SIM Application (for GSM networks)**
   * **Description**: The basic application needed to operate on GSM networks. It manages basic functions such as subscriber identification, authentication, and contact storage.
   * **Specification**: Defined by the GSM 11.11 specification.
2. **USIM Application (for UMTS networks)**
   * **Description**: Required for devices operating on UMTS (3G) networks. The USIM application enhances security features and supports more complex network functionalities compared to the basic SIM application.
   * **Specification**: Defined by the 3GPP TS 31.102 specification.

### **Development Considerations**

* **Protocol Variability**: Different networks and SIM card types (e.g., GSM, UMTS) use different communication protocols. SIM application developers must accommodate these variations to ensure compatibility across different networks.
* **Multi-Application UICCs**: Universal Integrated Circuit Cards (UICCs) can host multiple applications, such as SIM and USIM, allowing them to operate on both GSM and UMTS networks. Developers need to handle the presence of multiple applications and their interactions.

### **Contact Management**

* **Contact Storage**: Both SIM and USIM applications provide capabilities for storing contacts, known as Abbreviated Dialing Numbers (ADN).
* **Dual Application Data Handling**: In UICCs with both SIM and USIM applications, contacts may appear in both application contexts. However, the data is only stored once and referenced by both applications using file IDs. This approach avoids data duplication and allows efficient storage management.

### **Data Retrieval and Storage**

* **Pointer References**: Data can be stored with pointer references in volatile memory, allowing interaction with one application while being invisible to another.
* **File System Dumps**: Retrieving data from multi-application UICCs can be complex. A file system dump can provide more comprehensive information compared to a logical data dump. However, tools for performing such dumps are not commonly available anymore.

### **Key Specifications and Documentation**

* **3GPP TS 31.102**: This specification outlines the characteristics and requirements for USIM applications, providing essential guidelines for developers.
* **GSM 11.11**: Specifies the requirements for SIM applications in GSM networks.
* **Documentation**: Each major protocol and application type is extensively documented, offering detailed guidelines for developers to follow.

### Practical Applications

1. **Network-Specific Requirements**
   * **UMTS Networks**: Require USIM applications to leverage advanced features such as enhanced security and improved data management.
   * **GSM Networks**: Operate with basic SIM applications to provide essential network services.
2. **Device Compatibility**
   * **Modern Smartphones**: Often support both SIM and USIM applications, ensuring compatibility with both GSM and UMTS networks.
   * **IoT Devices**: May require specialized SIM applications to interact with specific network types and ensure reliable connectivity.
3. **Security and Data Management**
   * **Enhanced Security**: USIM applications offer improved security features, critical for protecting user data and ensuring secure communication.
   * **Efficient Data Handling**: Multi-application UICCs and advanced data referencing techniques allow for efficient storage and management of contact information and other data.

## Integrated Circuit Card ID (ICCID)

The ICCID (also referred to as the SIM/USIM header) value serves as a serial number for the UICC. This value is most often stored on the UICC itself and may provide authentication capabilities. The ICCID is often written on the back of the SIM card itself.

## ICCID Breakdown

Let Me Break It down for you:

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption><p>Breakdown... Breakdance... u get it..</p></figcaption></figure>

ICCID values range from 19-20 digits in length (20 bytes in length). The sequence of numbers directly represents a series of values used for authentication and diagnostic information. The ICCID value may be determined by appending each respective value in sequential order:

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption><p><strong>ICCID Breakdown Example</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption><p><strong>ICCID Breakdown</strong></p></figcaption></figure>

{% hint style="info" %}
**Simply it looks like this :**\
**ICCID** = System Code + Country Code + Issuer Identifier Number + UICC + Checksum
{% endhint %}



### System Code&#x20;

For SIM cards used in mobile devices, this value will be set to 89. This value indicates use by telecom providers. Defined in recommendation ITU-T E.164

### Country Code:&#x20;

Mobile number prefix (May range from 1-3 digits). E.g., United States and Canada country code = 1, United Kingdom = 44.

**For a complete list of country, codes see:** https://www.iban.com/dialing-codes

### Issuer Identification Number (IIN) :

Unique value to identify the carrier. (Verizon, AT\&T, T-Mobile, etc.)&#x20;

**Defined in ITU-T E.118**: [https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-REC-E.118-200605-I!!PDF-E\&type=items](https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-REC-E.118-200605-I!!PDF-E\&type=items)

### Unique identifier:&#x20;

A unique value associated to device user.&#x20;

### Checksum:&#x20;

The checksum value is determined by the Luhn Algorithm. This same algorithm is used to verify numerous identifiable numbers, namely credit card numbers. If the length of the ICCID is only 19 rather than 20 digits, then the last digit is filled in with the character ‘F’, this serves as a null character.&#x20;

**For an online Luhn number checker see**: https://www.dcode.fr/luhn-algorithm&#x20;

The ICCID value as stored on the mobile phone is saved in nibble swap order. This means that digits are grouped into pairs of two and then flipped. For further information on nibble swapping see HEX-120 Timestamp Formats. Nibble swap ordering is exemplified on the ICCID:

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption><p><strong>Nibble Swap Example</strong></p></figcaption></figure>

The ICCID value is available to the phone even if the device is PIN locked. The phone or an external SIM reading device will still have permission to read from the SIM card even if it is locked.

{% hint style="info" %}
If on an Apple iPhone the ICCID value may be found in the phone’s settings under&#x20;

**General > About > Primary > ICCID.**
{% endhint %}

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption><p><strong>iPhone Settings ICCID</strong></p></figcaption></figure>

## SIM Cloning

Some phones may lock out, or enter a “demo” mode, when a SIM card is missing. In this case, a SIM will be required before a phone is imaged or analyzed.&#x20;

To prevent network connection, a SIM Clone should be used. Special re-writable SIM clone cards allow for key identifiers, namely the Integrated Circuit Card ID (ICCID), to be written to the card while foregoing information which will connect a device to a network.&#x20;

More information on technical data formats will be discussed later.

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption><p>iPhone No SIM Card Notification</p></figcaption></figure>

### Recommended Video :

{% embed url="https://www.youtube.com/watch?v=JFpLGDmcx2g" %}

## SIM Cloning Tools

1. **Types of Tools**: Professional (paid) and freeware tools are available for SIM cloning, each operating differently and copying various segments of storage.
2. **Requirements**: These tools typically require an external SIM card reader for operation.
3. **Paid Toolkits**:
   * **XRY**: Offers SIM cloning capabilities with custom cloning SIM cards that are not compatible with Cellebrite UFED software.
   * **Cellebrite UFED**: Also provides SIM cloning functionalities with its own set of cloning SIM cards incompatible with XRY.
4. **MOBILedit SIM Cloning Tool**: Developed by Compelson, it allows users to selectively control which data is cloned to a new SIM card.

#### Details of MOBILedit SIM Cloning Tool

* **Tool Description**:
  * Version: 3.3.1
  * File Name: setup\_SIMClone\_3\_3\_1.exe
  * Purpose: Clone SIM Cards
  * MD5 Checksum: C3F1C21C131034DF0229A07F818A3494
  * [Download Link](https://download.mobiledit.com/mobiledit!/setup\_SIMClone\_3\_3\_1.exe)
* **Operating System Compatibility**: Supports 64-Bit Operating Systems: Windows 10/8/7/Vista/2000\*
* **Cloning Specifics**:
  * Cloning involves reading raw data from one SIM card and writing it to another. It does not recover direct data or perform imaging.
  * Cloned data cannot be transferred between different SIM cloning programs.
* **Unlocking Devices**: Inserting a clone SIM with stored keys and credentials may unlock a PIN/PUK locked device.
* **Creating Test SIMs**: If a phone is SIM-locked and discovered without a SIM installed, a test SIM can be created with specific settings to avoid data misinterpretation.

#### Cautionary Note

* **Data Integrity Concerns**: Never insert a personal SIM card into a phone for imaging purposes, as it can contaminate forensic analysis by syncing unintended data, as illustrated in a case involving a first responder's SIM.

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption><p><strong>MOBILedit SIM Cloning Tool</strong></p></figcaption></figure>

Certainly! Here's a more detailed combined overview of UICC imaging, incorporating the technical details provided:

## UICC Imaging

1. **Tools Required**: To recover data from a UICC (Universal Integrated Circuit Card), specialized imaging software and a compatible hardware card reader are essential.
2. **Tooling Types**:
   * **Forensic vs. Non-forensic Tools**:
     * **Forensic Tools**: These ensure data integrity by preventing any alterations during the imaging process.
     * **Non-forensic Tools**: While available, these tools may not guarantee data integrity and are typically used outside of forensic investigations.
3. **Data Retrieval Methods**:
   * Most tools interact with UICCs using Application Protocol Data Units (APDUs) at the application layer to perform logical dumps of data.
4. **Partition and Applications**:
   * UICCs are structured with multiple partitions and support various applications.
   * Applications such as USIM and SIM may store data like contacts and network information differently.
5. **Specific Tool Example - SIMIS**:
   * **Capabilities**: SIMIS provides read-only file system dump capabilities, allowing examination of SIM content and additional data parsing.
   * **Status**: Initially one of the first mobile forensic tools, SIMIS has been discontinued, impacting accessibility of its file system dumps.
6. **Challenges in UICC Imaging**:
   * **Complex Application Structure**: UICC applications lack standardization and are not user-friendly, requiring specific tools knowledgeable about their file hierarchy.
   * **File System Navigation**: Tools must anticipate data locations since UICCs lack a directory listing command.
   * **Tool Expertise**: Choosing a tool familiar with UICC structures and data locations is crucial for effective data retrieval and accurate forensic analysis.



Here's an organized summary of SIM card imaging tools, focusing on both non-forensic and forensic categories:

#### Non-Forensic SIM Card Imaging Tools

1. **Overview**:
   * Non-forensic SIM reading tools are often freeware but lack guarantees of data integrity. Careful testing and documentation are essential.
2. **Tools**:
   * **PYSIM**:
     * Used for reading and writing to programmable SIM and USIM cards.
     * Continuously updated on its GitHub repository.
   * **SIMBRUSH**:
     * Open-source Smart Card Forensics tool, though it may not always use forensically sound practices.
     * Requires manual compilation from its repository.
   * **SIMQUERY**:
     * CLI tool by Vidstrom Labs, displays ICCID and IMSI values from compatible SIM cards.
     * Compatible with generic Windows SIM card adapters, requires command-line execution.
   *   **UndeleteSMS**:

       * CLI tool from Vidstrom Labs, retrieves SMS messages from compatible SIM cards.
       * Requires command-line execution.

       <figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
   *   **GSIM Reader**:

       * Generic GSM reading application often bundled with physical SIM card readers.
       * Compatibility limited to specific devices bundled with the software.

       <figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>
   * **Dekart SIM Manager**:
     * Paid tool supporting various generic SIM card reader devices.
     * Offers a 30-day fully functional trial, features a user-friendly GUI.&#x20;
3. **Usage Considerations**:
   * Investigator-created methodologies ensure these tools are used in a forensically-sound manner.
   * Utilizing a variety of tools enhances investigative capabilities.

#### Forensic SIM Card Imaging Tools

1. **Overview**:
   * Forensic tools prohibit writing to SIM cards to maintain data integrity.
   * Specialize in pulling logical data and support various SIM applications.
2. **Tools**:
   * **Cellebrite UFED**
   * **Compelson MOBILedit Forensic**
   * **Magnet AXIOM**
   * **MSAB XRY**
   * **Oxygen Forensics Detective**
   * **SIMIS Tool**
   * **Susteen Secure View**
3. **Capabilities**:
   * Each tool excels in different aspects of SIM imaging, catering to diverse UICC applications.
   * Provide comprehensive capabilities for forensic analysis without altering original data.
4. **Toolbox Approach**:
   * Using multiple forensic tools enhances reliability and thoroughness in SIM card data extraction.
   * Ensures a robust approach to forensic investigations.

Here's a consolidated table that includes all the information for the freeware and open-source SIM card tooling:

<table data-header-hidden><thead><tr><th width="174"></th><th width="193"></th><th width="168"></th><th></th></tr></thead><tbody><tr><td><strong>Tool Name</strong></td><td><strong>Description</strong></td><td><strong>Download Link</strong></td><td><strong>Operating System</strong></td></tr><tr><td>pySIM</td><td>Python SIM card reader.</td><td><a href="https://github.com/osmocom/pySIM">GitHub - pySIM</a></td><td>Windows, Linux, and Mac OS</td></tr><tr><td>SIMBrush</td><td>Reads SIM card data.</td><td><a href="https://github.com/PicciMario/SIMBrush">GitHub - SIMBrush</a></td><td>Windows and Linux Operating Systems</td></tr><tr><td>SIMQuery</td><td>Retrieves ICCID and IMSI from GSM SIM cards.</td><td><a href="https://vidstromlabs.com/downloads/SIMquery.exe">Vidstrom Labs - SIMQuery</a></td><td>Windows ME or later</td></tr><tr><td>UndeleteSMS</td><td>Retrieves deleted messages from GSM SIM cards.</td><td><a href="https://vidstromlabs.com/downloads/undeletesms.exe">Vidstrom Labs - UndeleteSMS</a></td><td>Windows ME or later</td></tr><tr><td>GSIM Reader</td><td>Reads and writes data to SIM cards.</td><td><a href="http://www.mediafire.com/file/0e7zn8fiy2ahwr1/GSIMReaderApp_V1.0.7.2.rar/file">Mediafire - GSIM Reader</a></td><td>Windows ME or later</td></tr><tr><td>Dekart SIM Manager</td><td>Reads and modifies SIM data.</td><td><a href="https://www.dekart.com/free_download">Dekart - SIM Manager</a></td><td>Windows 98 or later</td></tr></tbody></table>



## **SIM PIN Lock**

SIM cards utilize a PIN lock mechanism to secure calling and text functionalities. Key points include:

* **Functionality**: Limits access to the SIM after three incorrect attempts, requiring the PUK.
* **Default PIN**: Carriers often set a default PIN that can be used if the user hasn't changed it.
* **Attempts**: Three attempts are allowed for entering the correct PIN.
* **PIN1 and PIN2**: Provide access to specific parts of the device based on cardholder verification (CHV1 and CHV2).

## **SIM PUK Lock**

After exhausting PIN attempts, the SIM prompts for a PUK to unlock completely:

* **Unlocking**: Correct entry of PUK enables full access and prompts for setting a new PIN.
* **Attempts**: Ten attempts are permitted for entering the correct PUK.
* **Permanent Lock**: After ten incorrect attempts, the SIM is permanently disabled.
* **Device Independence**: Attempts are not tied to a specific device; incorrect entries lock the SIM regardless of the device used.
* **Forensic Tools**: PUK entry from forensic tools counts towards attempts.

### **Retrieving PUK**

* **PUK Display**: Often printed on the SIM card frame at purchase.
* **Carrier Assistance**: Carriers can provide PUK with the ICCID, visible even when the SIM is locked.

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption><p><strong>T-Mobile SIM Card Frame</strong></p></figcaption></figure>

{% hint style="info" %}
**Understanding and managing SIM PIN and PUK locks is crucial for maintaining access to SIM functionalities while preventing accidental lockouts and permanent disablement.**
{% endhint %}



## **File Types on SIM Cards**

SIM cards utilize specific file types to organize data:

* **Master File (MF)**: The root directory on SIM cards, housing both Dedicated Files (DF) and Elementary Files (EF). It does not contain security permissions but serves as the main storage unit.
* **Dedicated File (DF)**: Sub-files within the MF directory, adhering to GSM11.11 standards. These files organize application-specific data and settings.
* **Elementary File (EF)**: Sub-files within DFs that store actual data used by applications, including contact information (like ICCID) and SMS messages. EFs are essential for forensic analysis as they contain actionable data.

File names are stored in ASCII format and are typically converted to hexadecimal for internal SIM card representation. They are either administrative, such as system files, or application-specific, containing user-generated data.

## **Encoding Methods**

SIM cards employ different encoding schemes for data representation:

* **7-bit Encoding**: Found in older SIM cards, used for SMS messaging and ADN (Abbreviated Dialing Number) data. This encoding optimizes storage space but requires conversion for non-GSM characters.
* **UCS-2 Encoding**: Utilized in modern SIM cards, a subset of UTF-16 encoding. UCS-2 supports a wider range of characters, crucial for international SMS and multilingual data storage.

### **SIM Security Features**

Security mechanisms within SIM cards protect sensitive information:

* **Master File Access**: Despite lacking direct security settings, access to DFs and EFs is controlled by Card Holder Verification (CHV) codes (PIN and PUK).
* **Card Holder Verification (CHV)**: Codes like PIN1 and PIN2 authenticate users and determine access levels to specific DFs and EFs. These codes are essential for accessing protected data stored on the SIM.

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption><p><strong>SIM Security Levels</strong></p></figcaption></figure>

### **Data Types and Forensic Significance**

SIM cards store diverse data types essential for forensic analysis:

* **Security Mechanisms**: Includes the Individual Subscriber Authentication Key (Ki), used for network authentication and encryption.
* **Network and Carrier Information**: Contains IMSI (International Mobile Subscriber Identity), network authentication keys, and service provider details.
* **User Data**: Personal information such as contacts, SMS messages, and service-specific data (e.g., prepaid balance).
* **Identifiers**: Unique identifiers like ICCID (Integrated Circuit Card Identifier) and IMSI distinguish each SIM card.

### **Security Identifiers and Authentication**

During network authentication:

* **Ki Ciphering Key**: Used to authenticate with the network, ensuring secure communication. Forensic tools do not provide direct access to the Ki key stored on the SIM, maintaining security integrity.



## Network Information

Some information that must be relayed between the mobile device and carrier network are stored locally on the SIM card.

### International Mobile Subscriber Identifier (IMSI):

It is important not to confuse the IMSI for the ICCID. The ICCID only identifies a unique SIM card. The IMSI on the other hand essentially identifies the phone to the network to monitor and charge network usage. (Identifies your mobile plan account) ICCID values are between 14-15 digits in length. The IMSI is created by appending the Mobile Country Code, Mobile Network Code, and Mobile Subscriber Identifier. The MSIN value used to represent the user’s own phone number, but this is not always the case now.

{% hint style="info" %}
For MCC and MNC code correlation see: http://mcc-mnc.com/
{% endhint %}

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption><p><strong>National MSI Structure</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption><p><strong>International MSI (IMSI) Structure</strong></p></figcaption></figure>

## **Temporary IMSI (TIMSI)**

* **Purpose**: Ensures security by using a temporary identifier instead of your true IMSI during sessions.
* **Functionality**: Local to the Mobile Station Controller (MSC) & Visitor Location Record (VLR) for OTA security.
* **Multiplicity**: Can assign multiple TIMSIs for different OTA services simultaneously.

### **Location Information (LOCI)**

* **File Type**: Elementary file storing location-related data.
* **Contents**: Includes the Location Area Identifier (LAI), formed by MCC, MNC, and Location Area Code (LAC).
* **Persistence**: Retains the last known location until device shutdown, crucial for tracking and service continuity.

### **Forbidden Public Land Mobile Network (FPLMN)**

* **Usage**: Records failed attempts to access cell stations, aiding in network efficiency.
* **Contents**: Stores MNC and MCC of forbidden networks, helpful during travel to avoid unnecessary connection attempts.

## USER DATA

Some data must be stored locally to provide a friendly user experience. This data is not sent over by a network provider rather created by a user’s own device:

### Abbreviated dialing **number (ADN):**

An elementary file type that may not be modified or viewed by the network provider. Although often referred to as contacts, it is important to remember that the ADN is only a list of user-created contacts.

### Fixed dialang numbers (FDN):

A list of phone numbers for which the phone is permitted to call. If enabled, the phone may only send outgoing calls to the phone numbers in this list. The phone may still receive incoming calls from any phone number. The FDN is missed by many tools; while investigating a SIM card you should ensure that the tools used will recover the FDN – it is essentially a secondary phonebook that may contain sensitive information.

### Last dialed numbers (LDN):

Listing of recently dialed calls. This listing is limited to a specific number of entries which may vary between applications. Some devices will store this information on the handset itself while some will store it on the UICC. Incoming calls are not stored in the LDN, only outgoing calls.

## Short Message Service (SMS):

The full length for an SMS storage entry is 176 bytes. The character limit for an SMS message is 160 characters (of the standard ASCII Latin alphabet), any message larger than this must be sent using an alternative protocol (MMS) or split into multiple messages. When large messages are split, it is possible for messages to be received in the incorrect order. Other alphabets which utilize a higher number of bits per character will be limited in sending capacity. The Unicode alphabet limits an SMS message to seven characters. It should be noted that Multimedia Messaging Service (MMS) messages are not stored on the SIM card, only on the device itself.&#x20;

The Short Message Service Center (SMSC) temporarily stores the SMS message until it is forwarded to the recipient. It is not forwarded until the recipients’ phone is on and looking for messages. While the recipient is not reachable the SMSC will wait an interval before trying again. This interval becomes exponentially longer as the recipient is not reached. The service center will wait several seconds before trying again and after some failed attempts will wait longer until seconds become minutes and minutes hours. This will continue until the waiting period becomes 72 hours at which point the message will be dropped from the center.&#x20;

The data retrieved from an SMS entry will contain the following information (in this order):

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption><p><strong>SMS Data Structure</strong></p></figcaption></figure>

The date and time value are stored in semi-octet and reverse nibble for the year, month, day, hour, minute, second, and time zone.

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption><p><strong>Exemplar Datetime Conversion</strong></p></figcaption></figure>

## Other identifiers

### Mobile subscriber integrated services digital network number / mobile station international subscriber directory number

#### Subscriber directory number (MSISDN):

An elementary file type that stores the SIM card’s unique telephone number. Phone numbers are no longer tied down to one mobile phone as they may now travel with the card itself. MSISDN data consists of the Country Code, National Destination Code, and Subscriber Number. The subscriber number is the SIMs’ number but not necessarily the phones’ number as more than one SIM could have been in a single device. If the MSISDN is blank, then the SIM card was never activated.

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption><p>MSISDN Structure</p></figcaption></figure>

### This table provides a detailed reference for commonly encountered acronyms in the field of digital forensics related to mobile telecommunications and SIM card analysis.

<table><thead><tr><th width="131">Acronym</th><th>Full Form</th><th>Description</th></tr></thead><tbody><tr><td>ETSI</td><td>European Telecommunications Standards Institute</td><td>Sets telecommunications standards in Europe and globally.</td></tr><tr><td>UICC</td><td>Universal Integrated Circuit Card</td><td>Smart card used in mobile devices.</td></tr><tr><td>SIM</td><td>Subscriber Identity Module</td><td>Contains subscriber information used for mobile communications.</td></tr><tr><td>USIM</td><td>Universal Subscriber Identity Module</td><td>Enhanced SIM card used in UMTS mobile networks.</td></tr><tr><td>R-UIM</td><td>Removable User Identity Module</td><td>Used in CDMA networks as an alternative to SIM cards.</td></tr><tr><td>CSIM</td><td>CDMA2000 Subscriber Identity Module</td><td>Specific SIM card used in CDMA2000 networks.</td></tr><tr><td>ICCID</td><td>Integrated Circuit Card Identifier</td><td>Unique identifier for SIM cards.</td></tr><tr><td>AND</td><td>Advanced Dialing Number</td><td>Service allowing complex dialing rules.</td></tr><tr><td>SMS</td><td>Short Messaging Service</td><td>Text messaging service for mobile phones.</td></tr><tr><td>LDN</td><td>Last Dialed Number</td><td>Record of the last dialed phone number.</td></tr><tr><td>3GPP</td><td>Third Generation Partnership Project</td><td>Standardization body for mobile telecommunications.</td></tr><tr><td>UMTS</td><td>Universal Mobile Telecommunications System</td><td>3G mobile network technology.</td></tr><tr><td>CDMA</td><td>Code Division Multiple Access</td><td>Technology used in some mobile networks.</td></tr><tr><td>PLMN</td><td>Public Land Mobile Network</td><td>Cellular network available to the public.</td></tr><tr><td>FPLMN</td><td>Forbidden Public Land Mobile Networks</td><td>List of networks barred from use.</td></tr><tr><td>FDN</td><td>Fixed Dialing Number</td><td>Numbers allowed for outgoing calls from a device.</td></tr><tr><td>MSISDN</td><td>Mobile Station ISDN Number</td><td>Phone number associated with a SIM card.</td></tr><tr><td>NPA</td><td>Number Planning Area</td><td>Geographic area code in the North American Numbering Plan.</td></tr><tr><td>SN</td><td>Subscriber Number</td><td>Unique number identifying a subscriber in a network.</td></tr><tr><td>MCC</td><td>Mobile Country Code</td><td>Three-digit code identifying a country in the ITU-T E.212 standard.</td></tr><tr><td>CC</td><td>Country Code</td><td>Standardized two-letter code identifying a country.</td></tr><tr><td>IMSI</td><td>International Mobile Subscriber Identity</td><td>Unique identifier for mobile subscribers.</td></tr><tr><td>MNC</td><td>Mobile Network Code</td><td>Identifies a mobile network operator within a country.</td></tr><tr><td>MSIN</td><td>Mobile Subscriber Identity Number</td><td>Portion of IMSI identifying a subscriber within a network.</td></tr><tr><td>TMSI</td><td>Temporary Mobile Subscriber Identity</td><td>Temporary identifier to enhance subscriber privacy.</td></tr><tr><td>APDU</td><td>Application Protocol Data Unit</td><td>Command/response pair in smart card communications.</td></tr><tr><td>CHV</td><td>Card Holder Verification</td><td>Security mechanism to authenticate SIM card users.</td></tr><tr><td>SPN</td><td>Service Provider Name</td><td>Name of the mobile network operator.</td></tr><tr><td>LP</td><td>Language Preference</td><td>Preferred language setting on a SIM card.</td></tr><tr><td>LAI</td><td>Local Area Identity</td><td>Identifies the area covered by a cellular network cell.</td></tr><tr><td>SMSC</td><td>Short Message Service Center</td><td>Central hub for SMS messages in a mobile network.</td></tr></tbody></table>



## References:

1. **ETSI**, "Secure Elements (Smart Cards)," ETSI, \[Online]. Available: [https://www.etsi.org/technologies/smart-cards](https://www.etsi.org/technologies/smart-cards). \[Accessed 15 07 2022].
2. **ETSI**, "ETSI TS 102 223 V17.0.0 (2022-05)," ETSI, \[Online]. Available: [https://www.etsi.org/deliver/etsi\_ts/102200\_102299/102223/17.00.00\_60/ts\_102223v17](https://www.etsi.org/deliver/etsi\_ts/102200\_102299/102223/17.00.00\_60/ts\_102223v17). \[Accessed 15 07 2022].
3. **s. varun**, "Smart Card (SIM Card) interface pinout," 30 05 2017. \[Online]. Available: [http://pinoutguide.com/Memory/SmartCardIso\_pinout.shtml](http://pinoutguide.com/Memory/SmartCardIso\_pinout.shtml). \[Accessed 14 Jul 2022].
4. **3GPP**, "3GPP," 22 01 2015. \[Online]. Available: [https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specifica](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specifica)tionId=1803. \[Accessed 15 07 2022].
5. **I. T. Union**, "ITU-T Rec. E.164 (11/2010) The international public telecommunication numbering plan," \[Online]. Available: [https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-RECE.164-201011-I!!PDF-E\&type=items](https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-RECE.164-201011-I!!PDF-E\&type=items). \[Accessed 15 07 2022].
6. **IBAN**, "LIST OF INTERNATIONAL COUNTRY CALLING PHONE CODES," IBAN, 17 07 2020. \[Online]. Available: [https://www.iban.com/dialing-codes](https://www.iban.com/dialing-codes). \[Accessed 15 07 2022].
7. **I. T. Union**, "ITU-T Rec. E.118 (05/2006) The international telecommunication charge card," \[Online]. Available: [https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-REC-E.118-200605-I!!PDF-E\&type=items](https://www.itu.int/rec/dologin\_pub.asp?lang=e\&id=T-REC-E.118-200605-I!!PDF-E\&type=items). \[Accessed 15 07 2022].
8. **Compelson**, "SIM Cloning Tool," MOBILedit, \[Online]. Available: [https://www.mobiledit.com/SIM-cloning](https://www.mobiledit.com/SIM-cloning). \[Accessed 15 07 2022].
9. **osmocom**, "osmocom/pySIM," \[Online]. Available: [https://github.com/osmocom/pySIM](https://github.com/osmocom/pySIM). \[Accessed 15 07 2022].
10. **A. Vidstrom**, "Vidstrom Labs," \[Online]. Available: [https://vidstromlabs.com/](https://vidstromlabs.com/). \[Accessed 15 07 2022].
11. **"GSM 7-bit Alphabet,"** CodeSegment, \[Online]. Available: [https://www.codesegment.com/GSM-alphabet.htm](https://www.codesegment.com/GSM-alphabet.htm). \[Accessed 18 07 2022].
12. **"Mobile Country Codes (MCC) and Mobile Network Codes (MNC),"** interactive digital media GmbH, \[Online]. Available: [http://mcc-mnc.com/](http://mcc-mnc.com/). \[Accessed 18 07 2022].
13. **M. Svein Yngvar Willassen**, "Forensics and the GSM mobile telephone system," 2003. \[Online]. Available: [https://www.utica.edu/academic/institutes/ecii/publications/articles/A0658858-BFF6-C537-7CF86A78D6DE746D.pdf](https://www.utica.edu/academic/institutes/ecii/publications/articles/A0658858-BFF6-C537-7CF86A78D6DE746D.pdf). \[Accessed 15 07 2022].
14. **dCode**, "Luhn Number Checksum," dCode, \[Online]. Available: [https://www.dcode.fr/luhn-algorithm](https://www.dcode.fr/luhn-algorithm). \[Accessed 15 07 2022].
