---
aliases: ["waterflow grid", "staggered grid"]
---
MOC:  [[SwiftUI|SwiftUI]]
GitHub: https://github.com/lichb0rn/StaggeredGrid

---

Сетка плохо работает с большими динамическими массивами.
Если нужно загружать много картинок (пробовал больше 2000), то грузить будет все!

### Код
```swift
import SwiftUI


struct ItemPreferenceData: Equatable {
    let id: AnyHashable
    let size: CGSize
}

struct ItemPreferenceKey: PreferenceKey {
    typealias Value = [ItemPreferenceData]
    
    static var defaultValue: [ItemPreferenceData] = []
    
    static func reduce(value: inout [ItemPreferenceData], nextValue: () -%3E [ItemPreferenceData]) {
        value.append(contentsOf: nextValue())
    }
}

struct ItemPreferenceSetter%3CID: Hashable>: View {
    var id: ID
    var body: some View {
        GeometryReader { proxy in
            Color.clear.preference(key: ItemPreferenceKey.self, value: [ItemPreferenceData(id: self.id, size: proxy.size)])
        }
    }
}
```

```swift
import SwiftUI

struct StaggeredGrid%3CContent: View, T: Hashable & Identifiable%3E: View {
    
    let cols: Int
    let spacing: CGFloat
    let gridItems: [T]
    let content: (T) -> Content
    
    @State private var gridHeight: CGFloat = 0
    @State private var alignmentGuides = [AnyHashable: CGPoint]()
    
    init(columnsCount: Int = 3, spacing: CGFloat = 8, gridItems: [T], @ViewBuilder content: @escaping (T) -> Content) {
        self.cols = columnsCount
        self.spacing = spacing
        self.gridItems = gridItems
        self.content = content
    }
    
    
    var body: some View {
        ScrollView(.vertical) {
            VStack {
                GeometryReader { proxy in
                    grid(in: proxy)
                        .onPreferenceChange(ItemPreferenceKey.self) { preferences in
                            let (alignmentGuides, gridHeight) = alignments(preferences: preferences)
                            
                            
                            self.alignmentGuides = alignmentGuides
                            self.gridHeight = gridHeight
                            
                        }
                }
            }
            .frame(height: gridHeight)
        }
    }
    
    private func grid(in geometry: GeometryProxy) -> some View {
        let columnWidth = max(0, geometry.size.width - (spacing * CGFloat(cols) - 1)) / CGFloat(cols)
        
        return ZStack(alignment: .topLeading) {
            ForEach(gridItems) { item in
                content(item)
                    .frame(width: columnWidth)
                    .background(ItemPreferenceSetter(id: item.id))
                    .alignmentGuide(.top, computeValue: {_ in self.alignmentGuides[item.id]?.y ?? 0 })
                    .alignmentGuide(.leading, computeValue: { _ in self.alignmentGuides[item.id]?.x ?? 0})
            }
        }
    }
    
    private func alignments(preferences: [ItemPreferenceData]) -> ([AnyHashable: CGPoint], CGFloat) {
        var heights = Array(repeating: CGFloat(0), count: cols)
        var alignmentGuides = [AnyHashable: CGPoint]()
        
        preferences.forEach { preference in
            if let minHeight = heights.min(), let idx = heights.firstIndex(of: minHeight) {
                
                let width = preference.size.width * CGFloat(idx) + CGFloat(idx) * spacing
                let height = heights[idx]
                
                let offset = CGPoint(x: 0 - width, y: 0 - height)
                heights[idx] += preference.size.height + spacing
                alignmentGuides[preference.id] = offset
            }
        }
        
        let gridHeight = max(0, (heights.max() ?? spacing) - spacing)
        return (alignmentGuides, gridHeight)
    }
}

struct StaggeredGrid_Previews: PreviewProvider {
    
    static var viewModels: [ComicGridItemViewModel] = {
        var vms = ComicItem.preview.map { item in
            let vm = ComicGridItemViewModel(comic: item)
            vm.isFetching = false
            return vm
        }
        return vms
    }()
    
    static var previews: some View {
        StaggeredGrid(gridItems: viewModels) { vm in
            ComicGridItemView(viewModel: vm)
        }
        .padding()
    }
}
```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
-  🏷️ Tags:: [[Design]], [[PreferenceKey]]