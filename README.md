# SwiftUI-Controls
 - [Segment](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#segment)
 - [Text and TabView](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#text-and-tabview)
 - [Stepper](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#stepper)
 - [Slider](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#slider)
 - [Date Picker](https://github.com/arjun011/SwiftUI-DatePicker)
 - [UIButton](https://github.com/arjun011/SwiftUI-Button)
 - [Form](https://github.com/arjun011/SwiftUI-Form)

# SwiftUI-Views
   - [Circle](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#circle-shape)
   - [Ellipse](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#ellipse)
   - [Trim Circle](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#circle-trim-shape)
   - [ActionSheet with isPresented](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#action-sheet-with-ispresented)
   - [ActionSheet with item](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#actionsheet-with-item)
   - [contextMenu](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#contextmenu)
   - [Offset](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#offset)
   - [Mask](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#mask)
   - [Rotation](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#rotation)
   - [LayOut Priority](https://github.com/arjun011/SwiftUI-Controls/blob/master/README.md#layout-priority)
   - [LazyHGrid](https://github.com/arjun011/LazyHGrid)

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

## Circle shape

    struct CircleCustomeTab: View {
      var body: some View {
        VStack(spacing: 15) {
            Text("Circle")
            Circle()
                .fill(Color.orange)
                .frame(width: 100)
            
            Circle()
                .stroke(Color.red, style: StrokeStyle(lineWidth: 4, dash: [9,5]))
                //.stroke(Color.red, lineWidth: 5)
                .frame(width:100)
                
            
            Circle()
                .foregroundColor(.green)
                .frame(width: 100)
            
            ZStack() {
                Circle()
                    .stroke(Color.red,lineWidth: 10)
                
                Circle()
                    .stroke(Color.yellow,lineWidth: 10)
                    .padding(20)
                
                Circle()
                    .stroke(Color.black,lineWidth: 10)
                    .padding(40)
                
                Circle()
                .stroke(Color.purple,lineWidth: 10)
                .padding(60)
                
                
            }.frame(width:200, height:200)
            
            ZStack {
                Circle()
                    .fill(Color.secondary)
                    .frame(height:250)
                Circle()
                    .fill(Color.secondary)
                    .frame(height:200)
                Circle()
                    .fill(Color.secondary)
                    .frame(height:150)
                Circle()
                    .fill(Color.secondary)
                    .frame(height:100)
            }
            
        }.padding()
     }
    }
    
   ### OutPut

![Screenshot 2020-02-19 at 6 14 57 PM](https://user-images.githubusercontent.com/16661905/74835850-3b89f580-5344-11ea-8357-448978192438.png)

### Ellipse
    
    struct EllipeCustomView: View {
      var body: some View {
        VStack(spacing:20) {
            Text("Ellips")
            Ellipse()
            
            ZStack {
                Ellipse()
                    .stroke(Color.yellow, lineWidth: 30)
                Ellipse()
                .stroke()
            }.padding()
            
            ZStack {
                Ellipse()
                    .strokeBorder(Color.pink,lineWidth: 30)
                Ellipse()
                    .stroke()
            }
            
            Spacer()
        }.padding()
      }
    }
    
   ## OutPut
   
   ![Screenshot 2020-02-19 at 6 15 06 PM](https://user-images.githubusercontent.com/16661905/74836253-0c27b880-5345-11ea-8415-34c3e6057632.png)
   
   ## Circle Trim shape
   
     struct TripOutLine: View {
        @State private var orangeCircleProgress:CGFloat = 0.9
        @State private var greenCircleProgress:CGFloat = 0.3
        private var percentage:Int {
        get {
            return Int(orangeCircleProgress * 100.0)
        }
    }
    var body: some View {
        VStack {
            Text("Circle Shape")
                .font(.largeTitle)
            Text("Trim function")
                .foregroundColor(.gray)
            
            ZStack {
                Circle()
                    .trim(from: 0.0, to: orangeCircleProgress)
                    .stroke(Color.orange, style: StrokeStyle(lineWidth: 40, lineCap: CGLineCap.round))
                    .frame(width:300)
                    .rotationEffect(.degrees(-90))
                    .overlay(
                        Text("\(percentage)%")
                )
                
                Circle()
                    .trim(from: 0.0, to: greenCircleProgress)
                    .stroke(Color.green, style: StrokeStyle(lineWidth: 40, lineCap: CGLineCap.round))
                    .frame(width:170)
                    .rotationEffect(.degrees(-90))
                    .overlay(
                        Text("\(percentage)%")
                )
            }
            .padding()
            Text("Completed Circle")
            Slider(value: $orangeCircleProgress)
                .padding(.horizontal)
                .accentColor(.orange)
            
            Slider(value: $greenCircleProgress)
                .padding(.horizontal)
                .accentColor(.green)
            
        }.font(.title)
            .padding()
      }
    }
    
   ### OutPut
   
   ![Screenshot 2020-02-19 at 6 14 52 PM](https://user-images.githubusercontent.com/16661905/74838668-fd8fd000-5349-11ea-864b-1226ead4efeb.png)
   
   ## Action Sheet with isPresented
   
    struct ContentView: View {
     @State private var openActionsheet:Bool = false
     var body: some View {
        VStack(spacing:20) {
            Text("Action Sheet")
            Button(action: {
                self.openActionsheet = true
            }) {
                Text("Open Action Sheet")
            }
        }.actionSheet(isPresented: $openActionsheet) { () -> ActionSheet in
           ActionSheet(title: Text("Hello!"), message: Text("This is action sheet."), buttons: [
            .default(Text("Action1"), action: {
                // Action 1
            }),
            .default(Text("Action2"), action: {
                // Action 2
            }),
            .destructive(Text("Red"), action: {
                // Action 3
            }),
            .cancel({
                // Cancel
            })
           ])
        }
      }
    }

### OutPut

 ![Screenshot 2020-02-24 at 5 25 29 PM](https://user-images.githubusercontent.com/16661905/75150839-49b48900-572b-11ea-8a31-7436fc539017.png)
 
 ## ActionSheet with item
 
    // Create Identifiable struct to hold action sheet data.
     struct ActionSheetData:Identifiable {
       var id = UUID()
       var title:String
       var message:String
     }
    struct customDataAction: View {
      @State private var actionSheetData: ActionSheetData? = nil
      var body: some View {
        VStack(spacing:20) {
            Text("Action Sheet")
                .font(.largeTitle)
            Text("Action with custom data")
                .foregroundColor(.gray)
            Button(action: {
                self.actionSheetData = ActionSheetData(title: "Save", message: "Choose an option!")
            }) {
                Text("Open Action sheet")
            }
        }.actionSheet(item: $actionSheetData) { sheetData in
            ActionSheet(title: Text(sheetData.title), message: Text(sheetData.message), buttons: [
                .default(Text("Default Option"), action: {
                    //Option 1
                }),
                .destructive(Text("Destructive Option"), action: {
                    // Destructive option
                }),
                .cancel({
                    // Cancel
                })
            ])
          }
       }
    }
   
 ### OutPut
 
 ![Screenshot 2020-02-24 at 5 25 58 PM](https://user-images.githubusercontent.com/16661905/75153089-80d96900-5730-11ea-873e-9b90c1f05dac.png)
 
 ## ContextMenu 
 
    struct ContentView: View {
     var body: some View {
        VStack(spacing:10) {
            Text("Context Menu")
                .font(.largeTitle)
            Text("Introduction")
                .foregroundColor(.gray)
            Spacer()
            HStack() {
                Text("Get Help")
                Spacer()
                Image(systemName: "questionmark.diamond.fill")
                    .foregroundColor(.yellow)
                    .contextMenu {
                        Button(action: {}) {
                            Image(systemName: "eyedropper.full")
                            Text("Add Color")
                        }
                        Button(action: {}) {
                            Image(systemName: "sun.haze")
                            Text("Haze")
                        }
                        Button(action: {}) {
                            Image(systemName: "circle.lefthalf.fill")
                            Text("Change Constrast")
                        }
                }
            }.padding()
            Spacer()
        }.font(.title)
      }
    }
    
  ### OutPut
  
  ![Screenshot 2020-03-05 at 1 38 47 PM](https://user-images.githubusercontent.com/16661905/75962635-26879780-5eea-11ea-8258-012a563691aa.png)
  
  ## Offset 
  
           VStack(spacing: 20) {
            Text("Offset")
                .font(.largeTitle)
            ZStack {
                RoundedRectangle(cornerRadius: 10)
                    .frame(width: 200, height: 100)
                    .foregroundColor(.green)
                    .shadow(radius: 5)
                    .offset(x: -20, y: -10)
                
                RoundedRectangle(cornerRadius: 10)
                .frame(width: 200, height: 100)
                .foregroundColor(.blue)
                .shadow(radius: 5)

                RoundedRectangle(cornerRadius: 10)
                .frame(width: 200, height: 100)
                .foregroundColor(.red)
                .shadow(radius: 5)
                .offset(x: 20, y: 20)
                
            }
        }
        
  ### Output
  
  ![Screenshot 2020-03-11 at 6 08 08 PM](https://user-images.githubusercontent.com/16661905/76417878-acf91900-63c3-11ea-8c0e-995368251cfe.png)

## Mask 

    struct ContentView: View {
      var body: some View {
        VStack {
            Text("Mask")
                .font(.largeTitle)
            Text("Mask is use to cut out background with other view ")
                .padding()
                .frame(maxWidth: .infinity)
                .background(Color.orange)
            
            Image("Flag-India")
                .resizable()
                .scaledToFill()
                .frame(width: 100, height: 100)
                .mask(Circle())
            
            Image("images")
                .resizable()
                .frame(width: 100, height: 100)
                .mask(
                    Text("INDIA")
                        .fontWeight(.black)
                        .font(.largeTitle)
            )
            Image("images")
                .resizable()
                .frame(width: 100, height: 100)
                .mask(Image(systemName: "tortoise").resizable())
            Spacer()
            
        }
     }
    }
    
### Output 

![Screen Shot 2020-04-23 at 1 53 55 PM](https://user-images.githubusercontent.com/16661905/80076597-1004d080-856a-11ea-94b0-479c89c84d73.png)

## Rotation 
     struct ContentView: View {
       @State var degree:Double = 360
       var body: some View {
        
        VStack(spacing: 30) {
            Text("Rotation")
                .font(.largeTitle)
            HStack {
                Text("45")
                    .rotationEffect(Angle.degrees(45))
                Text("-45")
                    .rotationEffect(Angle.degrees(-45))
                Text("90")
                    .rotationEffect(Angle.degrees(90))
                Text("180")
                    .rotationEffect(Angle.degrees(180))
                Text("270")
                    .rotationEffect(Angle.degrees(270))
                Text("360")
                    .rotationEffect(Angle.degrees(360))
            }
            Spacer()
            
            Text("Rotation")
                .font(.caption)
                .padding()
                .rotationEffect(Angle.degrees(degree))
                .border(Color.orange)
            
            HStack {
                Text("Top Rotation")
                    .font(.caption)
                    .padding()
                    .rotationEffect(Angle.degrees(degree), anchor: .top)
                    .border(Color.orange)
                
                Text("TopLeading Rotation")
                    .font(.caption)
                    .padding()
                    .rotationEffect(Angle.degrees(degree), anchor: .topLeading)
                    .border(Color.orange)
            }
            
            HStack {
                Text("Bottom Rotation")
                    .font(.caption)
                    .padding()
                    .rotationEffect(Angle.degrees(degree), anchor: .bottom)
                    .border(Color.orange)
                
                Text("BottomLeading Rotation")
                    .font(.caption)
                    .padding()
                    .rotationEffect(Angle.degrees(degree), anchor: .bottomLeading)
                    .border(Color.orange)
            }
            
            Slider(value: $degree, in: 0...360, step: 5.0)
                .padding()
            Text("\(degree, specifier: "%.2f") Degree")
            Spacer()
         }
      }
    }
    
### Output 

![Screenshot 2020-04-24 at 10 49 45 AM](https://user-images.githubusercontent.com/16661905/80177448-6bda6280-8619-11ea-8c93-1b4dd19a51ab.png)

## Layout Priority 
     default value is 0
     .layoutPriority(0)
     
     struct ContentView: View {
      var body: some View {
           HStack(alignment: .center, content: {
              Text("Hello World")
              Text("SwiftUI")
                  .foregroundColor(.blue)
              Text("It's a next future")
                  .layoutPriority(1)
          }).font(.title)
          .lineLimit(1)
        }
      }
### Output

<img width="194" alt="Screenshot 2021-10-18 at 2 26 31 PM" src="https://user-images.githubusercontent.com/16661905/137700840-64b7fa1c-08cd-4fdb-8470-38808cdee93b.png">



