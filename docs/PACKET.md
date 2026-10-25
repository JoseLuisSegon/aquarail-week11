# PACKET — WEEK 11 SHIP: AquaRail (Loss Visibility & Operational Dispatch Rail)

## 1. Problem in My Words
Mexican municipal water utilities lose up to 46% of water in transit due to unmonitored secondary network leaks and fragmented paper/WhatsApp dispatches. Current solutions either attempt automated diagnostic AI (unreliable and legally risky) or consumer tip apps (forbidden/ineffective).

## 2. Exact User
Field Crew Leaders (*Jefes de Cuadrilla*) and Municipal Utility Operations Dispatchers managing field response logistics.

## 3. Success Definition
Before the module closes, the application continuously ingests simulated pressure/acoustic sensor telemetry, flags anomaly deltas without automated engineering diagnosis, routes a 2-stage verification ticket to the field supervisor, logs photo/inspection confirmation, and updates operational state in real time.

## 4. Mermaid Flow Diagram
```mermaid
flowchart TD
    subgraph Sensing Layer [IoT & Route Telemetry]
        A[Pressure / Vibration Sensor Feed] -->|Variance Delta Triggered| B[AquaRail Ingestion Node]
    end

    subgraph System Engine [Dispatch & State Machine]
        B --> C{Operational Rule Engine}
        C -->|Logistical Routing Only| D[Create Verification Ticket]
    end

    subgraph Field Logistics [Human-in-the-Loop]
        D --> E[Jefe de Cuadrilla Interface]
        E -->|Dispatch Spot Inspector| F[Physical Site Inspection]
        F -->|Upload Photo & Confirm Leak| G[Human Diagnostic Logged]
        G -->|Release Repair Crew| H[Site Isolated & Repaired]
        H -->|Close Ticket| I[Recalibrate Node Baseline]
    end
5. Benchmark Line
The best existing solution on Earth for this is TaKaDu, which provides enterprise-grade SCADA network analytics. Mine differs and localizes by providing a lightweight, offline-first mobile dispatch rail designed for unmapped secondary networks and non-SCADA municipal operations in Mexico.
6. Long-View Paragraph (3-Year Vision)
In 3 years, AquaRail becomes the default open-source operational operating system for municipal infrastructure dispatches in Latin America. It bridges informal field repair work with municipal infrastructure planning by mapping invisible water losses in real time. Eventually, it expands into multi-utility dispatch for power grids and circular material tracking across secondary urban hubs.
7. Scope Cut (What I am NOT building)
NO automated AI structural pipe diagnosis (strictly zero symptom-checker logic; engineering judgment remains human).
NO consumer-facing leak reporting or awareness tips.
NO physical pipe-tapping hardware (using simulated sensor streams).
8. Architecture & Stack Table
Layer	Tech / Tool
Frontend	Next.js 14, Tailwind CSS, Lucide Icons (Deployed on Vercel)
Backend & Database	Supabase (PostgreSQL + Row Level Security)
Authentication	Supabase Auth (Sign in with Google)
Telemetry Simulation	Webhook / Interactive Telemetry Simulator Engine
9. Security Floor Checklist
[x] API Keys stored strictly in Vercel Environment Variables.
[x] Supabase Auth (Google Sign-In) enabled for user rows.
[x] Row Level Security (RLS) ON for all active tables.
[x] Input sanitization and length limits on forms.
[x] 100% synthetic/mock data used in live demonstration.
10. Test Plan
Mechanical Pass: Test sensor trigger threshold -> ticket creation -> RLS database write -> supervisor approval -> ticket close. Log and fix 1 bug in state synchronization.
Persona Pass: Test application with synthetic persona "Don Beto" (58-year-old senior field supervisor with low tech-literacy) to identify UX friction points.
