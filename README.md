# SwiftUI-Controls
 - [Segment](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#segment)
 - [Text and TabView](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#text-and-tabview)
 - [Stepper](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#stepper)
 - [Slider](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#slider)
 - [Date Picker](https://github.com/arjun011/SwiftUI-DatePicker)
 - [UIButton](https://github.com/arjun011/SwiftUI-Button)
 - [Form](https://github.com/arjun011/SwiftUI-Form)
## Segment 
 
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
    
 ### Output
 
 ![Screenshot 2020-02-18 at 1 58 39 PM](https://user-images.githubusercontent.com/16661905/74718519-67c84800-5258-11ea-90d0-78b60002ff92.png)
 
 ## Text and TabView 

    struct FontDesign: View {
     var body: some View {
        NavigationView {
            VStack(spacing: 10) {
                Text("Default font design")
                        .font(Font.system(size:30, design: .default))
                Divider()
                Text("Monospaced font design")
                    .font(Font.system(size:30, design: .monospaced))
                Divider()
                Text("Rounded font design")
                    .font(Font.system(size:30, design: .rounded))
                Divider()
                Text("Serif font design")
                    .font(Font.system(size:30, design: .serif))
                Divider()
                
                .navigationBarTitle(Text("Design"))
            }.padding()
        }
     }
    }

    struct TextStyle: View {
     var body: some View {
        NavigationView {
            VStack(spacing:10) {
                Text("Large Title").font(.largeTitle)
                Text("Title").font(.title)
                Text("Headline").font(.headline)
                Text("SubHeadline").font(.subheadline)
                Text("Body").font(.body)
                Text("Callout").font(.callout)
                Text("Caption").font(.caption)
                Text("FootNote").font(.footnote)
            }
        .navigationBarTitle(Text("Text Styles"))
        }
      }
    }

    struct WeightStyle: View {
     var body: some View {
        NavigationView {
            VStack(spacing:10) {
                Text("Ultralight").fontWeight(.ultraLight)
                Text("Thin").fontWeight(.thin)
                Text("Light").fontWeight(.light)
                Text("Regular").fontWeight(.regular)
                Text("Medium").fontWeight(.medium)
                Text("SemiBold").fontWeight(.semibold)
                Text("Bold").fontWeight(.bold)
                VStack(spacing:10) {
                    Text("Heavy").fontWeight(.heavy)
                    Text("Black").fontWeight(.black)
                }
            }
        .navigationBarTitle(Text("Weight"))
        }
      }
    }


    struct ContentView: View {
      @State var selectedTab = 0
      var body: some View {
         TabView(selection:$selectedTab) {
            TextStyle().tabItem {
               Image(systemName: "textformat")
                Text("Styles")
            }.tag(0)
            WeightStyle().tabItem {
                Image(systemName: "bold")
                Text("Weight")
            }.tag(1)
            FontDesign().tabItem {
                          Image(systemName: "text.cursor")
                          Text("Design")
                      }.tag(2)
          }
       }
    }

### OutPut 

 ![Screenshot 2020-02-18 at 2 32 03 PM](https://user-images.githubusercontent.com/16661905/74720699-2e91d700-525c-11ea-842c-e1a0d233f238.png)
![Screenshot 2020-02-18 at 2 31 56 PM](https://user-images.githubusercontent.com/16661905/74720701-305b9a80-525c-11ea-93e8-4e6d61e97259.png)
![Screenshot 2020-02-18 at 2 31 44 PM](https://user-images.githubusercontent.com/16661905/74720702-30f43100-525c-11ea-8786-32b44d82e125.png)

## Stepper 

    struct ContentView: View {
     @State private var stepperValue = 1
     @State private var values = [0,1]
     var body: some View {
        VStack(spacing:20) {
            Text("Stepper")
                .font(.largeTitle)
            Stepper(value: $stepperValue) {
                Text("Bound Stepper: \(stepperValue)")
            }
            
            Stepper(onIncrement: {
                self.values.append(self.values.count)
            }, onDecrement: {
                self.values.removeLast()
            }) {
                Text("OnIncrement and OnDecrement")
            }
            ScrollView(.horizontal) {
                HStack {
                    ForEach(values, id: \.self) { value in
                        Image(systemName: "\(value).circle.fill").font(.largeTitle)
                            .foregroundColor(.green)
                    }
                }.padding()
            }
            Stepper(value: $stepperValue, in: 1...5) {
                Text("Rating")
            }.padding(.horizontal)
            HStack {
                ForEach(1...stepperValue, id: \.self) { star in
                    Image(systemName: "star.fill")
                        .foregroundColor(.yellow)
                 }
             }
         }.padding()
      }
    }

### OutPut 

![Screenshot 2020-02-18 at 2 48 46 PM](https://user-images.githubusercontent.com/16661905/74721993-32bef400-525e-11ea-9d00-7f4e57aa34e6.png)

## Slider 

    struct ContentView: View {
    @State private var age = 18.0
    @State private var sliderValue = 0.3
    let ageFormatter: NumberFormatter = {
        let numFormate = NumberFormatter()
        numFormate.numberStyle = .spellOut
        return numFormate
    }()
    var body: some View {
        VStack(spacing:20){
            Text("Slider")
            Slider(value: $age, in: 1...100, step: 1)
            Group {
                Text("Age: ") + Text("\(ageFormatter.string(from: NSNumber(value: age))!)").foregroundColor(.green)
            }
            
            Slider(value: $sliderValue)
                .padding(.horizontal)
                .background(Color.yellow)
                .cornerRadius(10)
                .shadow(color: .gray, radius: 5)
                .accentColor(Color.green)
            
            Slider(value: $sliderValue)
                .padding(.horizontal)
                .background(Capsule().stroke(Color.orange, lineWidth: 2))
                .accentColor(.orange)
            
            Slider(value:$sliderValue)
                .padding(.horizontal)
                .background(Capsule().fill(Color.yellow))
                .accentColor(.black)
            
            HStack {
                Image(systemName: "tortoise")
                Slider(value:$sliderValue)
                Image(systemName: "hare")
            }.padding()
                .foregroundColor(.green)
            Spacer()
        }.padding()
     }
    }
   
   ## OutPut

![Screenshot 2020-02-18 at 2 58 50 PM](https://user-images.githubusercontent.com/16661905/74722658-4dde3380-525f-11ea-8e4c-102cd6905bd2.png)


   
