# Módulo `vpc`

Crea la capa de red base en AWS: VPC con DNS habilitado, subnets públicas y privadas distribuidas en varias AZ, Internet Gateway, tabla de rutas pública con sus asociaciones y un Security Group para acceso SSH restringido.

## Uso

```hcl
module "vpc" {
  source = "git::https://github.com/mdelrio96/EFT-Modulos-AUY1104-MDR.git//modules/vpc?ref=v1.0.0"

  project_name     = "eft"
  environment      = "dev"
  allowed_ssh_cidr = "203.0.113.10/32"
}
```

## Variables de entrada

| Nombre | Tipo | Default | Descripción |
|---|---|---|---|
| `project_name` | `string` | — | Prefijo de nombres de los recursos. |
| `environment` | `string` | — | Entorno de despliegue (dev, qa, prod). |
| `cidr_block` | `string` | `10.1.0.0/16` | CIDR principal de la VPC. |
| `availability_zones` | `list(string)` | 3 AZ de us-east-1 | AZs para las subnets. |
| `public_subnet_cidrs` | `list(string)` | 3 CIDRs /24 | CIDRs de subnets públicas. |
| `private_subnet_cidrs` | `list(string)` | 3 CIDRs /24 | CIDRs de subnets privadas. |
| `allowed_ssh_cidr` | `string` | — | Único CIDR autorizado para SSH (puerto 22). |

## Outputs

| Nombre | Descripción |
|---|---|
| `vpc_id` | ID de la VPC creada. |
| `public_subnet_ids` | IDs de las subnets públicas. |
| `private_subnet_ids` | IDs de las subnets privadas. |
| `subnet_ids` | IDs de todas las subnets (públicas + privadas). |
| `ssh_security_group_id` | ID del Security Group SSH (consumido por el módulo `ec2`). |
