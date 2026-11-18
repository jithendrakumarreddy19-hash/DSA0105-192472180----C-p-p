# Intelligent Medicine Expiry Prevention and Redistribution System Using C++

A C++17 HTTP server with a static HTML/CSS/JavaScript dashboard. Medicine and pharmacy records are stored in CSV files and exposed through read-only API endpoints.

## Requirements

- A C++17 compiler
- Windows networking library support (`Ws2_32`, included with MinGW-w64 or Visual Studio)
- Internet access for the stylesheet's Google Fonts; the dashboard otherwise works with local fonts

`backend/httplib.h` is the official single-header [cpp-httplib](https://github.com/yhirose/cpp-httplib) library. No package manager is required.

## Build and run with MinGW-w64

Open PowerShell in this project directory (`MedicineExpirySystem/`):

```powershell
g++ -std=c++17 -O2 backend/main.cpp -o backend/medicine-expiry-server.exe -lws2_32
.\backend\medicine-expiry-server.exe
```

Keep the server's working directory at this project root so it can find `frontend/` and `data/`. Open [http://localhost:8080](http://localhost:8080) in a browser. Stop the server with `Ctrl+C`.

## Build with Visual Studio

Run these commands from a Developer PowerShell prompt in this project directory:

```powershell
cl /std:c++17 /EHsc backend\main.cpp /Fe:backend\medicine-expiry-server.exe Ws2_32.lib
.\backend\medicine-expiry-server.exe
```

## API

- `GET /api/health` returns the server status as JSON.
- `GET /api/medicines` returns `data/medicines.csv` as CSV.
- `GET /api/pharmacies` returns `data/pharmacies.csv` as CSV.

The dashboard loads both CSV endpoints when it starts. Add records beneath the header row to populate the inventory and pharmacy views. Use ISO dates (`YYYY-MM-DD`) for `expiry_date`.

## CSV columns

`data/medicines.csv`:

```text
medicine_id,name,category,batch_number,quantity,expiry_date,pharmacy_id
```

`data/pharmacies.csv`:

```text
pharmacy_id,name,address,phone,contact_email
```

The starter API is read-only. Add validation and access controls before using it with real pharmacy or patient data.
