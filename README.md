# DXF → Graph Converter

DXF 파일을 방향성 그래프(JSON)로 변환하는 독립 모듈입니다.

## 의존성 설치
```bash
pip install ezdxf
```

## 사용법
```bash
python graph_maker.py
```
- 입력: `Drawing1.dxf` (기본값, 코드 하단 `__main__`에서 변경 가능)
- 출력: `graph.json`

## 파이프라인 구조

| 함수 | 역할 |
|---|---|
| `load_dxf_lines(filename)` | DXF에서 LINE/ARC 엔티티를 세그먼트 리스트로 추출 |
| `build_nodes_edges(segments)` | 세그먼트 → 노드/엣지 (좌표 기반 중복 제거, 소수점 3자리 반올림) |
| `build_directed_graph(nodes, edges)` | BFS + dot product 기반으로 방향 부여 |
| `save_graph(nodes, edges, filename)` | `graph.json`으로 저장 |

## 출력 포맷 (graph.json)
```json
{
  "nodes": [[x1, y1], [x2, y2], ...],
  "edges": [
    {"start": 0, "end": 1, "dir": [0, 1]},
    ...
  ]
}
```

## 샘플 파일
- `Drawing1.dxf` — 기본 테스트용 레이아웃
- `Encoded_layout.dxf` — 인코딩된 실제 레이아웃
