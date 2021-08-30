# CountTimer

![](https://github.com/comcxx11/CountTimer/blob/main/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-30%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.07.34.png)

```swift
class ViewController: UIViewController {
    
    @IBOutlet weak var lblTimer: UILabel!
    
    var seconds = 1800
    var timer: Timer?

    override func viewDidLoad() {
        super.viewDidLoad()
        
        startTimer()
    }
    
    private func startTimer() {
        countDown(isFirst: true)
        timer?.invalidate()
        timer = Timer.scheduledTimer(timeInterval: 1, target: self, selector: #selector(countDown), userInfo: nil, repeats: true)
    }

    @objc func countDown(isFirst: Bool = false) {
        if seconds == 0 {
            timer?.invalidate()
            lblTimer.text = ""
            return
        }
        
        if !isFirst {
            seconds = seconds - 1
        }
        
        let hour    = seconds / 3600
        let min     = (seconds % 3600) / 60
        let sec     = (seconds % 3600) % 60
        
        lblTimer.text = printTimer(hour, min, sec)
    }
    
    func printTimer(_ hour: Int, _ min: Int, _ sec: Int) -> String? {
        let h = singleToDouble(target: hour)
        let m = singleToDouble(target: min)
        let s = singleToDouble(target: sec)
        if hour == 0 && min == 0 {
            return "\(sec)"
        } else if hour == 0 {
            return "\(m):\(s)"
        } else if hour > 0 {
            return "\(h):\(m):\(s)"
        } else {
            return nil
        }
    }
    
    private func singleToDouble(target: Int) -> String {
        return (String(target).count == 1) ? "0\(target)" : String(target)
    }
}


```
