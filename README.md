# EXIF Data Extractor & Mapper

**A Digital Forensics Tool for Metadata Analysis and Visual Intelligence**

A browser-based forensic tool that extracts EXIF metadata from images, detects anomalies, clusters photos by location and visual similarity using AI, and provides reverse image search capabilities.

---

## 🎯 Purpose

When investigating digital evidence, metadata often tells stories that visible image content cannot. This tool helps forensic examiners, investigators, and security professionals:

- **Extract comprehensive metadata** from digital photographs (GPS, timestamps, camera settings)
- **Detect anomalies** that might indicate tampering or suspicious activity
- **Visualize geographic patterns** by clustering photos on interactive maps
- **Identify visual similarities** using machine learning to find duplicates, edits, or related images
- **Maintain chain of custody** with manual verification steps for external searches

Built as a digital forensics course project(EP2780 Digital forensics and incident response), this tool demonstrates how modern web technologies and AI can make forensic analysis more accessible.

---

## ✨ Key Features

### 📊 Comprehensive Metadata Extraction
- Extracts 40+ EXIF fields including camera make/model, GPS coordinates, timestamps, shooting parameters
- Supports JPEG and PNG image formats
- Batch processing for multiple images simultaneously
- Calculates derived values (megapixels, aspect ratios, authenticity scores)

### 🚨 Automated Anomaly Detection
- **Missing GPS Data**: Flags images without location information
- **Future Timestamps**: Detects impossible dates suggesting clock manipulation
- **Date Mismatches**: Identifies discrepancies between EXIF and file system dates
- **Metadata Completeness**: Assesses whether EXIF data appears stripped or incomplete

### 🗺️ Geographic Intelligence
- Interactive map visualization using Leaflet.js
- Automatic clustering of photos taken within 1km radius
- Color-coded markers showing photo density at each location
- One-click links to Google Maps for each cluster
- Movement pattern analysis across multiple locations

### 🤖 AI-Powered Visual Similarity
- Uses TensorFlow.js and MobileNet CNN for feature extraction
- Identifies visually similar images even with different metadata
- Groups photos into clusters with similarity scoring
- Detects potential duplicates, edits, screenshots, or related images
- **100% offline operation** - no data sent to external servers

### 🔍 Reverse Image Search Integration
- Manual upload workflow maintaining forensic chain of custody
- Integration with Google Images, TinEye, and Yandex
- AI-powered local search compares against uploaded batch offline
- Clear documentation for legal admissibility

### 📄 Comprehensive Reporting
- Detailed forensic analysis reports in plain text format
- JSON export for integration with other tools
- CSV export with full metadata and cluster assignments
- Cross-image comparison tables
- Complete EXIF tag dumps for court documentation

---

## 🚀 Quick Start

### Prerequisites
- Modern web browser (Chrome 90+, Firefox 88+, Edge 90+, Safari 14+)
- JavaScript enabled
- No installation required!

### Usage

1. **Download the HTML file** or open it in your browser
2. **Click "Choose Files"** and select one or more images (JPEG/PNG)
3. **Wait for processing** - the tool will automatically:
   - Extract all EXIF metadata
   - Detect anomalies
   - Run AI clustering analysis
   - Generate geographic maps (if GPS data present)
4. **Review results** in the interactive interface
5. **Generate reports** using the export buttons

### Example Workflow

```
1. Upload 20 vacation photos from a suspect's phone
2. Tool extracts metadata and identifies 3 geographic clusters
3. AI clustering reveals 2 groups of visually similar images
4. Anomaly detection flags 3 images with missing GPS data
5. Generate comprehensive forensic report for case file
6. Export CSV for timeline analysis in Excel
```

---

## 📖 Detailed Feature Guide

### Statistics Panel

The statistics summary provides immediate intelligence about your image set:

- **Total Images**: Number of files processed
- **With GPS Data**: Percentage containing location information
- **Unique Devices**: How many different cameras/phones were used
- **Date Range**: Time span covered by the photos
- **Anomalies Found**: Count of potential issues detected
- **AI Clusters**: Number of visual similarity groups identified
- **Location Clusters**: Geographic groupings within 1km

### Anomaly Detection Explained

**Missing GPS Data**
- Not always suspicious (older cameras, GPS disabled)
- Consistent across all images = likely device limitation
- Selective missing GPS = possible deliberate removal

**Future Timestamps**
- Physically impossible dates (e.g., 2026 when it's 2025)
- Usually indicates incorrect device clock settings
- Could indicate metadata manipulation

**Date Mismatches**
- Large gaps between EXIF date and file modification date
- Can occur from editing, file transfers, or metadata stripping
- Differences >30 days flagged as suspicious

### AI Visual Similarity Clustering

The tool uses MobileNet (pre-trained on ImageNet) to extract 1024-dimensional feature vectors from each image, then calculates cosine similarity between all pairs:

**Similarity Scores:**
- **80-100%**: Nearly identical (duplicates, minor edits, crops)
- **65-79%**: Moderately similar (same scene, similar subjects)
- **Below 65%**: Considered dissimilar

**Forensic Applications:**
- Finding multiple versions of the same photo (original + edited)
- Identifying screenshots or re-photographs
- Grouping photos from the same event/location
- Detecting images that should be related but have different metadata

### Geographic Clustering

Photos with GPS coordinates are automatically grouped by proximity:

**Cluster Algorithm:**
- Uses Haversine formula for accurate distance calculation
- Groups images within 1km radius
- Calculates cluster centroids for multi-image groups
- Color-codes markers by density (red = 5+ photos, orange = 3-4, blue = 1-2)

**Use Cases:**
- Tracking subject movement over time
- Verifying alibi locations
- Identifying frequented locations
- Correlating photos from different sources at same scene

### Reverse Image Search

**AI-Powered Local Search (Recommended):**
- Compares against all images in current batch
- 100% offline - no data leaves your computer
- Instant results with similarity percentages
- No API costs or rate limits

**Manual External Search:**
- Downloads image and opens search engine
- User manually uploads to Google/TinEye/Yandex
- Maintains chain of custody through documented manual process
- Appropriate for sensitive or confidential evidence

**Why Manual Upload?**
- Chain of custody: Every action documented and authorized
- Privacy protection: Investigator reviews before external upload
- Legal compliance: Meets court requirements for evidence handling
- Security: Prevents automated exposure of sensitive material

---

## 🏗️ Technical Architecture

### Frontend Stack
```
HTML5 + CSS3 + Vanilla JavaScript
├── EXIF.js (metadata extraction)
├── Leaflet.js (interactive mapping)
├── TensorFlow.js 4.11.0 (ML framework)
└── MobileNet 2.1.0 (CNN model)
```

### Key Design Decisions

**Client-Side Processing**
- All computation happens in the browser
- No data sent to external servers (except manual searches)
- Works offline after initial page load
- No installation or dependencies required

**No LocalStorage/SessionStorage**
- Data exists only in memory during session
- Automatic cleanup when page closes
- No persistent storage of evidence
- Prevents data leakage or unauthorized access

**Modular Architecture**
```javascript
handleFiles()           // File input processing
extractExifData()       // EXIF parsing
detectAnomalies()       // Forensic checks
performAIClustering()   // ML similarity analysis
clusterByLocation()     // Geographic grouping
generateReport()        // Report generation
```

### Performance Characteristics

| Image Count | Processing Time | Memory Usage |
|-------------|----------------|--------------|
| 1-10        | 5-10 seconds   | ~50MB        |
| 11-25       | 15-25 seconds  | ~100MB       |
| 26-50       | 30-45 seconds  | ~200MB       |
| 51-100      | 60-90 seconds  | ~400MB       |

*Times include AI feature extraction on mid-range laptop (Intel i5, 8GB RAM)*

---

## 🎓 Educational Value

This project demonstrates understanding of:

### Digital Forensics Concepts
- Metadata analysis and EXIF interpretation
- Chain of custody and evidence integrity
- Anomaly detection and suspicious pattern identification
- Geographic intelligence from GPS data
- Forensic reporting standards

### Technical Skills
- JavaScript file handling and binary data processing
- Machine learning model integration (TensorFlow.js)
- Geospatial calculations (Haversine distance)
- Data visualization (maps, tables, charts)
- Report generation and data export

### Legal/Procedural Awareness
- Evidence handling best practices
- Privacy and confidentiality considerations
- Manual verification requirements
- Audit trail documentation

---

## 📊 Comparison to Professional Tools

### vs. ExifTool (Industry Standard)

**ExifTool Advantages:**
- Supports 100+ file formats (RAW, video, documents)
- Extracts 1000+ metadata fields
- Camera-specific maker notes
- Decades of development and testing
- Command-line scriptability

**This Tool's Advantages:**
- Visual interface (no command-line required)
- Interactive maps for GPS visualization
- AI-powered similarity clustering
- Automatic anomaly detection
- Batch processing with visual feedback
- Accessible to non-technical users

**Bottom Line:** This tool complements ExifTool by providing visual analysis and automated pattern detection, but doesn't replace its comprehensive extraction capabilities.

---

## 🔒 Security and Privacy

### Data Handling
- **All processing happens locally** in your browser
- **No data sent to external servers** (except manual searches you authorize)
- **No cookies or tracking**
- **No persistent storage** - data cleared when page closes
- **No telemetry or analytics**

### Forensic Integrity
- **Manual verification** for external searches maintains chain of custody
- **Audit trail** can be maintained through screen recording/documentation
- **Hash verification** recommended before processing (not built-in)
- **Read-only operation** - never modifies original files

### Limitations
- Not a certified forensic tool
- No formal audit logging
- No cryptographic hash verification
- No write-blocking mechanisms
- Not suitable for high-stakes legal proceedings without additional documentation

---

## 🐛 Known Limitations

### Technical Constraints
- **Format Support**: Only JPEG and PNG (no RAW, video, or documents)
- **EXIF Coverage**: ~40 common fields (not comprehensive like ExifTool)
- **Browser Memory**: Large batches (100+ images) may cause performance issues
- **File Size**: Very large images (>20MB) process slowly

### Forensic Gaps
- No formal chain of custody documentation
- No cryptographic integrity verification
- No audit logging system
- No integration with forensic databases
- Reports not in standard forensic formats

### AI Limitations
- MobileNet trained for object recognition, not forensic analysis
- Similarity thresholds may need adjustment for specific use cases
- Black-box model can't fully explain similarity decisions
- May miss forensically relevant but visually dissimilar connections

---

## 🚧 Future Enhancements

### Planned Features
- [ ] SHA-256 hash verification before/after processing
- [ ] Formal audit log with timestamps and user actions
- [ ] RAW format support (CR2, NEF, ARW)
- [ ] Video metadata extraction (MP4, MOV)
- [ ] Timeline visualization with temporal gap detection
- [ ] Reverse geocoding (GPS → street addresses)
- [ ] Batch archive processing (ZIP, RAW)
- [ ] Custom report templates
- [ ] Database export for forensic suites



---

## ⚖️ Legal Disclaimer

**IMPORTANT: This tool is provided for educational and research purposes only.**

- This is NOT certified forensic software
- User is responsible for proper evidence handling and chain of custody
- No warranty or guarantee of accuracy

**By using this tool, you acknowledge:**
- You have proper authorization to analyze the images
- You will maintain proper chain of custody procedures
- You understand the legal requirements in your jurisdiction
- You will not rely solely on this tool for critical forensic determinations

---

## 🙏 Acknowledgments

### Inspiration and Learning Resources
- **ExifTool** by Phil Harvey - The gold standard that inspired this project
- **Autopsy Digital Forensics** - For forensic workflow insights
- **NIST Computer Forensics Tool Testing** - For understanding validation requirements
- **SWGDE Guidelines** - For forensic best practices

### Test Images Used
https://github.com/ianare/exif-samples?tab=readme-ov-file

### Technical Libraries
- **EXIF.js** - JavaScript EXIF extraction
- **Leaflet.js** - Beautiful open-source mapping
- **TensorFlow.js** - Making ML accessible in browsers
- **MobileNet** - Efficient image classification
- **OpenStreetMap** - Free geographic data

### Educational Context
- Built for Digital Forensics course at KTH
- Demonstrates both technical skills and forensic awareness

---

## 🎯 Project Goals: Achieved

- [x] Extract comprehensive EXIF metadata from images
- [x] Detect forensic anomalies automatically
- [x] Cluster photos by geographic location
- [x] Implement AI-powered visual similarity analysis
- [x] Provide reverse image search capabilities
- [x] Maintain proper forensic protocols
- [x] Generate comprehensive reports
- [x] Create accessible, user-friendly interface
- [x] Complete project in one week
- [x] Learn digital forensics principles deeply

---
