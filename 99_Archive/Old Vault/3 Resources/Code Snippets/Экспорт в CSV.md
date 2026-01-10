---
aliases: ['export to csv']
---

# Экспорт данных из [[Core Data|CoreData]] в csv

Пример того, как это можно сделать.

1. Собираем данные модели:

````swift
    func csv() -> String {
        let coalescedHeight = height ?? ""
        let coalescedPeriod = period ?? ""
        let coalescedWind = wind ?? ""
        let coalescedLocation = location ?? ""
        let coalescedRating: String
        if let rating = rating?.int16Value {
            coalescedRating = String(rating)
        } else {
            coalescedRating = ""
        }

        return [
            stringForDate(),
            coalescedHeight,
            coalescedPeriod,
            coalescedWind,
            coalescedLocation,
            coalescedRating,
            "\n"
        ].joined(separator: ",")
    }```

2. Делаем запрос и экспортируем в csv
```swift

    func exportCSVFile() {
        navigationItem.leftBarButtonItem = activityIndicatorBarButtonItem()

        coreDataStack.storeContainer.performBackgroundTask { context in
            var results: [JournalEntry] = []
            do {
                results = try context.fetch(self.surfJournalFetchRequest())
            } catch let error as NSError {
                print("ERROR: \(error.localizedDescription)")
            }
            // 2
            let exportFilePath = NSTemporaryDirectory() + "export.csv"
            let exportFileURL = URL(fileURLWithPath: exportFilePath)
            FileManager.default.createFile(atPath: exportFilePath, contents: Data(), attributes: nil)

            // 3
            let fileHandle: FileHandle?
            do {
                fileHandle = try FileHandle(forWritingTo: exportFileURL)
            } catch let error as NSError {
                print("ERROR: \(error.localizedDescription)")
                fileHandle = nil
            }

            if let fileHandle = fileHandle {
                // 4
                for journalEntry in results {
                    fileHandle.seekToEndOfFile()
                    guard let csvData = journalEntry
                            .csv()
                            .data(using: .utf8, allowLossyConversion: false) else {
                                continue
                            }

                    fileHandle.write(csvData)
                }

                // 5
                fileHandle.closeFile()

                print("Export Path: \(exportFilePath)")
                DispatchQueue.main.async {
                    self.navigationItem.leftBarButtonItem = self.exportBarButtonItem()
                    self.showExportFinishedAlertView(exportFilePath)
                }
            } else {
                DispatchQueue.main.async {
                    self.navigationItem.leftBarButtonItem = self.exportBarButtonItem()
                }
            }
        }
    }
````

Метод выполняется **асинхронного**, не блокируя UI на главном потоке.


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: 
-  🏷️ Tags:: [[Core Data|CoreData]]