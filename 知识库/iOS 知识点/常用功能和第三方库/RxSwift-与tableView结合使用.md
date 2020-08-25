# RxSwift与TableView结合使用

## 数据模型

```swift
//
//  JLMusic.swift
//  RxSwiftPractice
//
//  Created by Joya Wang on 2020/8/24.
//  Copyright © 2020 Joya Wang. All rights reserved.
//

import Foundation

struct JLMusic {
    let name: String //歌名
    let singer: String //演唱者
     
    init(name: String, singer: String) {
        self.name = name
        self.singer = singer
    }
}

extension JLMusic: CustomStringConvertible {
    var description: String {
        return "name：\(name) singer：\(singer)"
    }
}
```





## 视图模型

```swift
//
//  JLMusicListViewModel.swift
//  RxSwiftPractice
//
//  Created by Joya Wang on 2020/8/24.
//  Copyright © 2020 Joya Wang. All rights reserved.
//

import Foundation
import RxSwift


struct JLMusicListViewModel {
    
    let data = Observable.just([
        JLMusic(name: "无条件", singer: "陈奕迅"),
        JLMusic(name: "你曾是少年", singer: "S.H.E"),
        JLMusic(name: "从前的我", singer: "陈洁仪"),
        JLMusic(name: "在木星", singer: "朴树"),
    ])
    
}

```



## 使用RxSwift将数据和TableView绑定

```swift
//
//  ViewController.swift
//  RxSwiftPractice
//
//  Created by Joya Wang on 2020/8/24.
//  Copyright © 2020 Joya Wang. All rights reserved.
//

import UIKit
import RxSwift
import RxCocoa

class ViewController: UIViewController {
    
    
    var tableView = UITableView()
    
    // 视图模型
    let musicListViewModel = JLMusicListViewModel()
    
    //负责对象销毁
    let disposeBag = DisposeBag()

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Do any additional setup after loading the view.
        view.addSubview(tableView)
        tableView.frame = UIScreen.main.bounds
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "musicCell")
        
        
        // 将数据源绑定到tableView上
        /*
         将视图模型的data数据绑定到tableView的items上，每个cell对应data中的一个music数据模型
         */
        musicListViewModel.data.bind(to: tableView.rx.items(cellIdentifier: "musicCell")){_,music,cell in
            cell.textLabel?.text = music.name
            cell.detailTextLabel?.text = music.singer
        }.disposed(by: disposeBag)
            
        
        // tableView点击响应
        tableView.rx.modelSelected(JLMusic.self).subscribe(onNext: { (music) in
            print("你选中的歌曲信息【\(music)】")
            }).disposed(by: disposeBag)
    }
    
}


```

