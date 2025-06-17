# Architecture Diagrams

This directory contains architecture diagrams for the Minikube and Snyk security testing setup.

## Diagram Files

- `minikube-snyk-architecture.png`: Overall architecture of the Minikube and Snyk setup
- `security-improvement-process.png`: Process flow for improving security of deployments
- `vulnerability-comparison.png`: Comparison of vulnerabilities across different deployments

## Minikube Snyk Architecture

This diagram shows the overall architecture of our setup, including:
- Local development environment with Docker
- Minikube cluster with basic and secure NGINX deployments
- Snyk security testing for IaC and container images

## Security Improvement Process

This diagram illustrates the process of improving security:
1. Initial deployment with basic NGINX
2. Scanning with Snyk to identify vulnerabilities
3. Improved deployment with Alpine-based image
4. Further scanning to identify remaining issues
5. Fully secure deployment with all security best practices

## Vulnerability Comparison

This diagram compares the vulnerabilities found in:
- Basic NGINX deployment (nginx:1.14.2)
- Secure NGINX deployment (nginx:1.28.0-alpine)
- Fully secure NGINX deployment (with security context)
