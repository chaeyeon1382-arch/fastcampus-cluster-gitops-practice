# Multi-Cloud Hybrid Kubernetes Cluster (Home PC + Oracle Cloud + AWS)

홈 PC, Oracle Cloud Free Tier, AWS를 WireGuard/Site-to-Site VPN으로 연결하여
하나의 Kubernetes 클러스터로 구성한 하이브리드 멀티클라우드 인프라 프로젝트입니다.

## 프로젝트 개요
- **Step 1**: 홈 PC(control-plane) ↔ Oracle Cloud(worker)를 WireGuard VPN으로 연결한 2노드 K8s 클러스터 구축, Argo CD 기반 GitOps 전환
- **Step 2**: Terraform으로 AWS 인프라를 코드화하고, Oracle·홈 네트워크와 Site-to-Site VPN(IPsec)으로 연결해 AWS EC2를 3번째 워커 노드로 추가한 멀티클라우드 확장

## 아키텍처
- Home PC (control-plane) — WireGuard VPN
- Oracle Cloud Free Tier (gateway/worker) — WireGuard + Site-to-Site VPN
- AWS (worker) — Terraform 프로비저닝 + Site-to-Site VPN(IPsec)
- CNI: Cilium / Ingress: ingress-nginx / GitOps: Argo CD

## 주요 구성 요소
- `apps/`, `values/`, `manifests/` — Argo CD GitOps 매니페스트 (Step 1)
- `aws-terraform/` — AWS 인프라 Terraform 코드 (Step 2)

## 기술 스택
Kubernetes, Cilium, Argo CD, WireGuard, Terraform, AWS, Oracle Cloud Infrastructure, IPsec VPN

## 참고 사항
- `manifests/wordpress/`의 DB 비밀번호는 실습 편의상 평문으로 두었습니다. 실제 운영 환경
에서는 Sealed Secrets 또는 External Secrets Operator로 관리해야 합니다.
- 실습 종료 후 AWS 리소스는 모두 삭제했습니다.

## 출처
이 프로젝트는 **패스트캠퍼스 [실전 DevOps의 모든 것: 리눅스부터 GitOps까지]** 강의의 실습 프로젝트를 기반으로 진행했습니다.
기본 구성은 강의 자료를 따르되, 직접 인프라를 구축하고 발생한 이슈(리소스 제약, IAM 권한, VPN 설정 오류 등)를 트러블슈팅하며 완성했습니다.
