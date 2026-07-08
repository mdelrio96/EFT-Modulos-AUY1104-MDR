# Módulo `s3`

Crea un bucket S3 con nombre parametrizado (único a nivel global) y tag de entorno.

## Uso

```hcl
module "s3" {
  source = "git::https://github.com/mdelrio96/EFT-Modulos-AUY1104-MDR.git//modules/s3?ref=v1.0.0"

  bucket_name = "eft-auy1104-mdr-bucket-unico"
  environment = "dev"
}
```

## Variables de entrada

| Nombre | Tipo | Default | Descripción |
|---|---|---|---|
| `bucket_name` | `string` | — | Nombre del bucket (único global). |
| `environment` | `string` | — | Entorno de despliegue, aplicado como tag. |

## Outputs

| Nombre | Descripción |
|---|---|
| `bucket_name` | Nombre del bucket creado. |
