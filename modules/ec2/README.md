# Módulo `ec2`

Crea una instancia EC2 con monitoreo detallado habilitado, pensada para el AWS Academy Learner Lab (`t2.micro` y key pair `vockey` por defecto).

## Uso

```hcl
module "ec2" {
  source = "git::https://github.com/mdelrio96/EFT-Modulos-AUY1104-MDR.git//modules/ec2?ref=v1.0.0"

  project_name       = "eft"
  environment        = "dev"
  subnet_id          = module.vpc.public_subnet_ids[0]
  security_group_ids = [module.vpc.ssh_security_group_id]
}
```

## Variables de entrada

| Nombre | Tipo | Default | Descripción |
|---|---|---|---|
| `project_name` | `string` | — | Prefijo de nombres de los recursos. |
| `environment` | `string` | — | Entorno de despliegue (dev, qa, prod). |
| `subnet_id` | `string` | — | Subnet de despliegue (pública si se requiere IP pública). |
| `security_group_ids` | `list(string)` | — | Security groups asociados a la instancia. |
| `ami_id` | `string` | `ami-0ec10929233384c7f` | AMI (Ubuntu en us-east-1). |
| `instance_type` | `string` | `t2.micro` | Tipo de instancia (restricción del laboratorio y de la política OPA). |
| `key_name` | `string` | `vockey` | Key pair del Learner Lab. |

## Outputs

| Nombre | Descripción |
|---|---|
| `instance_id` | ID de la instancia creada. |
| `instance_ip` | IP pública de la instancia. |
