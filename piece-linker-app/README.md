# Kustomize Application

This project demonstrates the use of Kustomize for managing Kubernetes configurations. It is structured to separate base resources from environment-specific overlays, allowing for easy customization and deployment.

## Project Structure

- **base/**: Contains the base Kubernetes resources.
  - **deployment.yaml**: Defines the Kubernetes deployment resource, including container image, CPU requests, and limits.
  - **kustomization.yaml**: Kustomize configuration for the base resources.

- **overlays/**: Contains environment-specific configurations.
  - **production/**: Configuration for the production environment.
    - **kustomization.yaml**: Kustomize configuration for the production overlay, referencing the base kustomization and specifying modifications such as image tag and resource limits.
    - **params.env**: Environment variables for parameterizing the Kustomize build, including the image tag and CPU requests and limits.

## Usage

1. **Install Kustomize**: Ensure you have Kustomize installed on your machine. You can find installation instructions in the [Kustomize documentation](https://kubectl.docs.kubernetes.io/).

2. **Build the Base Configuration**: Navigate to the base directory and run:
   ```
   kustomize build ./base
   ```

3. **Build the Production Overlay**: Navigate to the production overlay directory and run:
   ```
   kustomize build ./overlays/production
   ```

4. **Deploy to Kubernetes**: You can pipe the output of the Kustomize build directly to `kubectl` to deploy your resources:
   ```
   kustomize build ./overlays/production | kubectl apply -f -
   ```

## Parameters

The project uses environment variables defined in `params.env` to parameterize the Kustomize build. Modify these variables to change the image tag and resource limits as needed.

## Conclusion

This Kustomize application provides a flexible way to manage Kubernetes configurations across different environments, ensuring that deployments are consistent and easily adjustable.