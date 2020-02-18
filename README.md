# SwiftUI-Controls

## Segment ##
 
    struct ContentView: View {
        @State private var dayNight = "morning"
        @State private var tab = 0
        @State private var meals = "one"
    
    var body: some View {
        VStack(spacing: 20){
            Text("Segment")
                .font(.largeTitle)
            Picker(selection: $dayNight, label: Text("DayPiker")) {
                Text("Morning").tag("morning")
                Text("Noon").tag("noon")
                Text("Night").tag("night")
            }.labelsHidden()
                .pickerStyle(SegmentedPickerStyle())

            Picker(selection: $tab, label: Text("")) {
                Image(systemName: "sun.min").tag(0)
                Image(systemName: "moon").tag(1)
            }.pickerStyle(SegmentedPickerStyle())

            Picker(selection: $meals, label: Text("")) {
                Text("One").tag("one")
                Text("Two").tag("two")
                Text("Three").tag("three")
                Text("More").tag("more")
            }
            .background(Color.yellow)
                .cornerRadius(10)
                .padding(.horizontal)
                .pickerStyle(SegmentedPickerStyle())
                

            Spacer()
        }.padding()
      }
    }
    
 # Output
 
 ![Screenshot 2020-02-18 at 1 58 39 PM](https://user-images.githubusercontent.com/16661905/74718519-67c84800-5258-11ea-90d0-78b60002ff92.png)
