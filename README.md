## 1. Teoretické principy

Dijkstrův algoritmus je algoritmus pro hledání nejkratších cest v orientovaném nebo neorientovaném grafu s nezgápornými vahami hran. Funguje tak, že postupně vybírá vrchol s nejmenší známou vzdáleností, aktualizuje vzdálenosti sousedů a označí vrchol jako navštívený. Výsledkem jsou nejkratší vzdálenosti od zvoleného startovního vrcholu ke všem ostatním.

## 2. Kód

Celý projekt je napsaný v TypeScriptu a Reactu. Hlavní části:
- Komponenta `App.tsx` – uživatelské rozhraní, zadání grafu, spuštění algoritmu, vizualizace.
- Funkce `dijkstra` v `src/dijkstra.ts` – samotná implementace algoritmu.

### Ukázka hlavní části algoritmu:

```typescript
export function dijkstra(edges: Edge[], numVertices: number, start: number): number[] {
  const distances = Array(numVertices).fill(Infinity);
  distances[start] = 0;
  const visited = Array(numVertices).fill(false);
  while (true) {
    let closest = -1;
    let closestDist = Infinity;
    for (let i = 0; i < numVertices; i++) {
      if (!visited[i] && distances[i] < closestDist) {
        closestDist = distances[i];
        closest = i;
      }
    }
    if (closest === -1) break;
    visited[closest] = true;
    for (const edge of edges) {
      if (edge.from === closest) {
        const newDist = distances[closest] + edge.weight;
        if (newDist < distances[edge.to]) {
          distances[edge.to] = newDist;
        }
      }
    }
  }
  return distances;
}
```

## 3. Testovací data

Výchozí testovací data v aplikaci:

```
0 1 4
0 2 1
2 1 2
1 3 1
2 3 5
```

Počet vrcholů: 4
Startovní vrchol: 0

Výsledek: Nejkratší vzdálenosti od vrcholu 0 jsou [0, 3, 1, 4]

## 4. Grafy a vizualizace

Aplikace zobrazuje graf pomocí SVG – vrcholy jsou rozmístěné do kruhu, hrany jsou spojnice s popisem váhy. Výsledky algoritmu se zobrazují pod vstupem.
