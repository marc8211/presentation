@workspace /new
Générer les fichiers suivants pour un projet Infrastructure as Code utilisant Terraform sur Azure :

1. **Fichiers au niveau racine :**
    - `provider.tf` : Définir la configuration du fournisseur Terraform.
    - `variables.tf` : Gérer les variables globales.
    - `backend.tf` : Configurer le backend Terraform (ex. stockage Azure).
    - `README.md` : Documenter toute la solution en français. Il doit fournir une vue d'ensemble de la structure du projet et décrire l'objectif de chaque fichier et répertoire.
2. **Répertoire `/scripts` :**
    - `deploy_infra.ps1` : Déployer l'infrastructure Terraform via Azure PowerShell.
    - `destroy_infra.ps1` : Détruire l'infrastructure déployée.
    - `lint_infra.ps1` : Appliquer les standards de codage avec `terraform fmt`.
    - `test_infra_validation.ps1` : Valider le bon fonctionnement de l'infrastructure après déploiement.
3. **Répertoire `/modules` :**
    - **Module Synapse (`/synapse`) :**
        - `synapse_workspace.tf` : Définir la ressource du workspace Synapse. Le nom sera `synw-terraform-iac-{type_environnement}`.
        - `synapse_sql_dedicated_pool.tf` : Gérer le pool SQL dédié. Le nom sera `syndp-terraform-iac-{type_environnement}`.
        - `synapse_sql_serverless_pool.tf` : Configurer le pool SQL sans serveur. Le nom sera `synop-terraform-iac-{type_environnement}`.
        - `variables.tf` : Variables spécifiques au module.
        - `outputs.tf` : Valeurs de sortie du module Synapse.
    - **Module Data Lake (`/datalake`) :**
        - `datalake_gen2.tf` : Configurer la ressource Data Lake Gen2. Le nom sera `stterraformiac{type_environnement}`.
        - `variables.tf` : Variables spécifiques au module.
        - `outputs.tf` : Valeurs de sortie du module Data Lake.
    - **Module Key Vault (`/keyvault`) :**
        - `keyvault.tf` : Gérer les ressources Key Vault. Le nom sera `kv-terraform-iac-{type_environnement}`.
        - `variables.tf` : Variables spécifiques au module.
        - `outputs.tf` : Valeurs de sortie du module Key Vault.
    - **Module Resource Group (`/resource_group`) :**
        - `resource_group.tf` : Définir le groupe de ressources Azure. Le nom sera `rg-terraform-iac-{type_environnement}`.
        - `variables.tf` : Variables spécifiques au module.
        - `outputs.tf` : Valeurs de sortie du module Resource Group.
4. **Répertoire `/environments` :**
    - **Pour chaque environnement (`dev`, `qa`, `prod`) :**
        - `main.tf` : Fichier de configuration principal.
        - `variables.tf` : Variables spécifiques à l'environnement.
        - `provider.tf` : Configuration du fournisseur spécifique à l'environnement.
5. **Répertoire `/pipelines` :**
    - `pipeline_infra_deploy.yml` : Déployer automatiquement l'infrastructure Terraform.
    - `pipeline_infra_destroy.yml` : Détruire l'infrastructure via un pipeline CI/CD.
    - `pipeline_infra_lint.yml` : Appliquer les bonnes pratiques et validation de code (`terraform fmt`, `terraform validate`).
    - D'autres pipelines pour les tests et les validations de la configuration Terraform, si nécessaire.

Ces pipelines YAML doivent inclure des étapes pour :

- Installer les outils Terraform et Azure CLI.
- Valider la configuration (`terraform validate`).
- Planifier et appliquer le déploiement (`terraform plan` et `terraform apply`).
- Détruire l'infrastructure (`terraform destroy`) lorsque nécessaire.
- Gérer les erreurs et inclure des notifications (Slack, Teams, email).