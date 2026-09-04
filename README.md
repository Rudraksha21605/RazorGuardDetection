# RazorGuard — Fraud Detection & Risk Intelligence

RazorGuard is a component-based payment fraud detection platform built for the Razorpay Builderthon. It evaluates transactions in real time and returns an explainable APPROVE, CHALLENGE, or BLOCK decision.

## Architecture

React + TypeScript -> reusable UI components -> Spring Boot REST API -> RiskService -> RiskEngine -> TransactionRiskRepository -> H2

## Component-based frontend

- Header — navigation and product identity
- MetricCard — reusable dashboard metric
- RiskAssessmentForm — transaction input and demo scenarios
- RiskResult — decision, score, explanation, triggered rules and telemetry
- types.ts — shared TypeScript contracts

## Modular backend

- RiskController — REST API boundary
- RiskService — validation, persistence and orchestration
- RiskEngine — isolated explainable fraud scoring
- RiskRule — rule contribution model
- RiskAssessment — immutable decision model
- TransactionRiskRepository — fraud-signal queries and persistence

## Detection signals

| Signal | Trigger | Contribution |
|---|---|---:|
| Checkout velocity | More than 3 transactions in 60 seconds | Up to 55% |
| Device/account sharing | Fingerprint used by multiple accounts | 40% |
| High-value payment | Amount above INR 150,000 | 25% |
| Baseline | Every transaction starts from a low-risk baseline | 5% |

Decision thresholds: 0–39% APPROVE, 40–74% CHALLENGE, 75–100% BLOCK.

## API

- GET /api/v1/risk/health
- POST /api/v1/risk/assess

## Run locally

### Frontend
From the repository root:
npm install
npm run dev

Open http://localhost:5173.

### Backend
Open a second terminal in the same repository root:
mvn spring-boot:run

If Maven is not on PATH, use your local Maven executable, for example:
& "C:\Users\DELL\Downloads\apache-maven-3.9.16-bin\apache-maven-3.9.16\bin\mvn.cmd" spring-boot:run

Backend runs on http://localhost:8080.

Health check: http://localhost:8080/api/v1/risk/health

## Builderthon demo

1. Start the backend.
2. Start the frontend.
3. Click Normal for a low-risk transaction.
4. Click High value to demonstrate the high-value signal.
5. Reuse a fingerprint with different user IDs to demonstrate device sharing.
6. Submit the same user repeatedly to demonstrate velocity detection.
7. Show Triggered Signals to explain the decision.

## Tech stack

React 19, TypeScript, Vite, Lucide React, Spring Boot, Spring Data JPA, H2, Maven and Java 17.