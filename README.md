<h1 align="center">CR Directorio - Costa Rica Geographic Data</h1>

<p align="center">
  JSON data source for the <a href="https://github.com/AndresBol/BikerStriker">BikerStriker</a> desktop application.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Format-JSON-yellow?logo=json&logoColor=white" alt="JSON"/>
  <img src="https://img.shields.io/badge/Served%20via-GitHub%20Raw-black?logo=github&logoColor=white" alt="GitHub Raw"/>
  <img src="https://img.shields.io/badge/Provincias-7-blue" alt="Provincias"/>
  <img src="https://img.shields.io/badge/Cantones-81-green" alt="Cantones"/>
  <img src="https://img.shields.io/badge/Distritos-474-orange" alt="Distritos"/>
</p>

---

## Purpose

This repository hosts the **Costa Rica political division data** consumed by the [BikerStriker](https://github.com/AndresBol/BikerStriker) application. By externalizing the geographic directory into a separate repository, the data can be updated independently without modifying or redeploying the main project.

The main application fetches this data at runtime via the GitHub Raw Content API:

```
https://raw.githubusercontent.com/AndresBol/CR_Directorio/main/provincias.json
https://raw.githubusercontent.com/AndresBol/CR_Directorio/main/cantones.json
https://raw.githubusercontent.com/AndresBol/CR_Directorio/main/distritos.json
```

## Data Schema

### `provincias.json` - Provinces

| Field         | Type   | Description                |
| ------------- | ------ | -------------------------- |
| `IdProvincia` | number | Unique province identifier |
| `Descripcion` | string | Province name              |

```json
{
  "IdProvincia": 1,
  "Descripcion": "San Jose"
}
```

### `cantones.json` - Cantons

| Field         | Type   | Description                                           |
| ------------- | ------ | ----------------------------------------------------- |
| `IdCanton`    | number | Unique canton identifier (province prefix + sequence) |
| `IdProvincia` | number | Foreign key to the parent province                    |
| `Descripcion` | string | Canton name                                           |

```json
{
  "IdCanton": 101,
  "IdProvincia": 1,
  "Descripcion": "San José"
}
```

### `distritos.json` - Districts

| Field         | Type   | Description                                           |
| ------------- | ------ | ----------------------------------------------------- |
| `IdDistrito`  | number | Unique district identifier (canton prefix + sequence) |
| `IdCanton`    | number | Foreign key to the parent canton                      |
| `Descripcion` | string | District name                                         |

```json
{
  "IdDistrito": 10101,
  "IdCanton": 101,
  "Descripcion": "Carmen"
}
```

## Relationships

```
Provincia (7) → Canton (81) → Distrito (474)
```

Each province contains multiple cantons, and each canton contains multiple districts, following Costa Rica's official three-level political division.

## Related Repository

| Repository                                                | Description                                                         |
| --------------------------------------------------------- | ------------------------------------------------------------------- |
| [BikerStriker](https://github.com/AndresBol/BikerStriker) | Main desktop application - C#, WinForms, SQL Server, .NET Framework |

---

<p align="center">
  <sub>Data repository for the BikerStriker academic project - Universidad Técnica Nacional (UTN)</sub>
</p>
