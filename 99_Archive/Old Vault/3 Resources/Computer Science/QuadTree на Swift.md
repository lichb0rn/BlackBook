---
uuid: 20221030201120
created: 2022-10-30T20:11:20
alias:
- quadtree swift
- swift quadtree
tags:
---

# [[QuadTree на Swift]]

```swift
struct QuadTree {
    private var root: Node
    private(set) var count = 0
    
    init(region: CGRect) {
        root = Node(region: region)
    }
    
    @discardableResult
    mutating func insert(_ point: CGPoint) -> Bool {
        /*
         “isKnownUniquelyReferenced() returns true if there is only one instance.
         If there is more than one instance, you need to make a copy of the underlying tree.
         Then, you can add the point.
         */
        if !isKnownUniquelyReferenced(&root) {
            root = root.copy()
        }
        guard root.insert(point) else {
            return false
        }
        count += 1
        return true
    }
    
    func find(in searchRegion: CGRect) -> [CGPoint] {
        root.find(in: searchRegion)
    }
    
    // Simply delegates to the root node.
    // points() gathers all the points by finding them from the root node down.
    func points() -> [CGPoint] {
        find(in: root.region)
    }
    
    func regions() -> [CGRect] {
        collectRegions(from: root)
    }
    
    // Recursively gathers all the regions of all the nodes
    private func collectRegions(from node: Node) -> [CGRect] {
        var results = [node.region]
        if let quad = node.quad {
            results += quad.all.flatMap { collectRegions(from: $0) }
        }
        return results
    }
    
    /*
     The nested class Node will do the heavy lifting for QuadTree.
     Each node instance keeps a region and can hold up to four points (the bucket size)
     before it spills over and subdivides itself into four more nodes contained in Quad’s structure.
     */
    private final class Node {
        let maxItemCapacity = 4
        var region: CGRect
        var points: [CGPoint] = []
        var quad: Quad?
        
        init(region: CGRect, points: [CGPoint] = [], quad: Quad? = nil) {
            self.region = region
            self.quad = quad
            self.points = points
            self.points.reserveCapacity(maxItemCapacity)
            precondition(points.count <= maxItemCapacity)
        }
        
        
        struct Quad {
            var northWest: Node
            var northEast: Node
            var southWest: Node
            var southEast: Node
            
            var all: [Node] { [northWest, northEast, southWest, southEast] }
            
            init(region: CGRect) {
                let halfWidth = region.size.width * 0.5
                let halfHeight = region.size.height * 0.5
                
                northWest = Node(region: CGRect(x: region.origin.x,
                                                y: region.origin.y,
                                                width: halfWidth, height: halfHeight))
                northEast = Node(region: CGRect(x: region.origin.x + halfWidth,
                                                y: region.origin.y,
                                                width: halfWidth, height: halfHeight))
                southWest = Node(region: CGRect(x: region.origin.x,
                                                y: region.origin.y + halfHeight,
                                                width: halfWidth, height: halfHeight))
                southEast = Node(region: CGRect(x: region.origin.x + halfWidth,
                                                y: region.origin.y + halfHeight,
                                                width: halfWidth, height: halfHeight))
            }
            
            init(northWest: Node, northEast: Node, southWest: Node, southEast: Node) {
                self.northWest = northWest
                self.northEast = northEast
                self.southWest = southWest
                self.southEast = southEast
            }
            
            func copy() -> Quad {
                Quad(northWest: northWest.copy(),
                     northEast: northEast.copy(),
                     southWest: southWest.copy(),
                     southEast: southEast.copy())
            }
        }
        
        func copy() -> Node {
            Node(region: region, points: points, quad: quad?.copy())
        }
        
        func subdivide() {
            precondition(quad == nil, "Can't subdivide a node already subdivided")
            quad = Quad(region: region)
        }
        
        @discardableResult
        func insert(_ point: CGPoint) -> Bool {
            // Checks whether the node has been subdivided. If it has, the function attempts to insert the point into each one of the nodes in the quad.
            if let quad = quad {
                return quad.northWest.insert(point) ||
                    quad.northEast.insert(point) ||
                    quad.southWest.insert(point) ||
                    quad.southEast.insert(point)
            } else {
                // If the node is at maximum capacity, it subdivides the node and attempts the insert again.
                if points.count == maxItemCapacity {
                    subdivide()
                    return insert(point)
                } else {
                    // If the node is not at maximum capacity, it first checks whether the point falls inside the region the node is responsible for.
                    // If it does, it inserts it into the array of points and returns true.
                    guard region.contains(point) else {
                        return false
                    }
                    points.append(point)
                    return true
                }
            }
        }
        /*
         1. This code first checks whether the search region overlaps with the region the node is responsible for.
         If it doesn’t, it returns no points. This return is the base case of the recursion.
         2. Next, it filters the points in the region and adds them to the found list.
         3. Finally, if the node has been subdivided, it goes through the quads and recursively calls find(in:) to add points to the found list before returning it.
         */
        func find(in searchRegion: CGRect) -> [CGPoint] {
            guard region.intersects(searchRegion) else {
                return []
            }
            var found = points.filter { searchRegion.contains($0) }
            if let quad = quad {
                found += quad.all.flatMap { $0.find(in: searchRegion) }
            }
            return found
        }
    }
}

```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- ℹ️ Source:: [[Expert Swift]]