# SwiftUI-CustomFontView

```swift
struct ContentView: View {
        
    let alphabet: String = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    
    /*
    [
     "A": ["HELLO", "WORLD"],
     "B": ["HELLO", "WORLD"]
    ]
     */
    var fonts: [String: [String]] = [:]
    
    init() {
        UIFont.familyNames.forEach { fontName in
            for character in alphabet {
                if fontName.first == character {
                    if fonts.keys.contains(String(character)) {
                        fonts[String(character)]?.append(fontName)
                    } else {
                        fonts[String(character)] = [fontName]
                    }
                }
            }
        }
        print(fonts)
    }
    
    var body: some View {
        List {
            ForEach(fonts.map{ $0.key }.sorted(by: <), id: \.self) { title in
                Section(header: Text(title)) {
                    ForEach(fonts[title].map { $0 }!, id: \.self) { fontName in
                        Text(fontName)
                            .font(.custom(fontName, size: 16))
                    }
                }
            }
        }
        .listStyle(GroupedListStyle())
    }

}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

```
