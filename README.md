# UT-CORE-BOARDS

PCB designs and board requirements for UT-CORE.

## Structure

Each subsystem contains its boards. Each board has the same three folders:

```text
<subsystem>/<board>/
├── hardware/       # Existing KiCad projects and their supporting files
├── docs/           # Board requirements and existing documentation
└── datasheets/     # Component datasheets and manufacturer references
```

Keep KiCad projects, libraries, models, schematic sheets, and other project
dependencies together. Existing revision folders, backups, manufacturing
outputs, and simulations are preserved inside `hardware/`.

## Boards

| Subsystem | Board requirements | Hardware |
|-----------|--------------------|----------|
| ADCS | [Controller](ADCS/controller/docs/adcs-board-requirements.md) | [Projects](ADCS/controller/hardware/) |
| ADCS | [Motor](ADCS/motor/docs/motor-board-requirements.md) | [Projects](ADCS/motor/hardware/) |
| CDH | [Controller](CDH/controller/docs/cdh-board-requirements.md) | [Projects](CDH/controller/hardware/) |
| EPS | [Battery](EPS/battery/docs/battery-board-requirements.md) | [Projects](EPS/battery/hardware/) |
| EPS | [Solar panel](EPS/solar-panel/docs/solar-panel-board-requirements.md) | [Projects](EPS/solar-panel/hardware/) |
| EPS | [Solar conglomerator](EPS/solar-conglomerator/docs/solar-conglomerator-board-requirements.md) | [Projects](EPS/solar-conglomerator/hardware/) |
| EPS | [Magtest](EPS/magtest/docs/magtest-board-requirements.md) | [PCB](EPS/magtest/hardware/) |
| GNSS | [Receiver](GNSS/receiver/docs/gnss-board-requirements.md) | [Projects](GNSS/receiver/hardware/) |

Solar panel variants stay together under `EPS/solar-panel/hardware/`, with
their original project folders intact. Both battery project bundles are
preserved under `EPS/battery/hardware/`. The standalone `magtest.kicad_pcb`
is preserved separately; its purpose and status still are undocumented.

## Board documents

Use [the template](templates/name-board-requirements.md) and name each document
`<name>-board-requirements.md`, using lowercase words separated by hyphens.
Existing documents and sheets remain alongside them in `docs/` as references.

The five sections cover purpose and design, specifications, interfaces,
operation and limitations, and notes. Keep detailed implementation and design
history in the board files and PRs. Identify the applicable PCB revision and
mark unknown or unverified information clearly.

Existing project-local libraries and models have not been consolidated or
renamed. Any datasheets already embedded in a project should stay there if
moving them could affect references; the new `datasheets/` folders are for
standalone references.
