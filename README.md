# EFT-Modulos-AUY1104-MDR

Repositorio de módulos reutilizables de Terraform para el Examen Final Transversal de Infraestructura como Código II (Duoc UC).

Consolida el trabajo de las Evaluaciones Parciales 1, 2 y 3: infraestructura base en AWS desacoplada en módulos independientes, documentados y versionados semánticamente.

## Módulos

| Módulo | Descripción |
|---|---|
| [`modules/vpc`](modules/vpc/) | Red base: VPC, subnets públicas y privadas, Internet Gateway, tabla de rutas pública y Security Group SSH. |
| [`modules/ec2`](modules/ec2/) | Instancia EC2 `t2.micro` en subnet pública, asociada al Security Group de la capa de red. |
| [`modules/s3`](modules/s3/) | Bucket S3 con nombre parametrizado globalmente único. |

## Consumo desde un módulo raíz

Los módulos se consumen mediante *Git source* con tag de versión semántica:

```hcl
module "vpc" {
  source = "git::https://github.com/mdelrio96/EFT-Modulos-AUY1104-MDR.git//modules/vpc?ref=v1.0.0"

  project_name     = "eft"
  environment      = "dev"
  allowed_ssh_cidr = "203.0.113.10/32"
}
```

## Versionado

Los releases se gestionan con [release-please](https://github.com/googleapis/release-please) a partir de Conventional Commits:

- `feat:` → incremento MINOR
- `fix:` → incremento PATCH
- `feat!:` / `BREAKING CHANGE:` → incremento MAJOR
- `chore:`, `docs:`, `refactor:` → sin release

## Entorno

Diseñado para AWS Academy Learner Lab (`us-east-1`): instancias `t2.micro`, key pair `vockey` y restricciones propias del laboratorio.
