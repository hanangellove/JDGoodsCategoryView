    NSMutableArray * nameArray = [NSMutableArray arrayWithObjects:@"热搜榜",
                                                                  @"红酒馆",
                                                                  @"白酒馆",
                                                                  @"洋酒馆",
                                                                  @"滋补品",
                                                                  @"啤酒馆",
                                                                  @"黄酒馆",
                                                                  @"果酒馆",
                                                                  @"品酒小助手",
                                                                  nil];
    
    NSMutableArray * lis = [NSMutableArray arrayWithCapacity:0];
    /**
     *  构建需要数据 2层或者3层数据 (ps 2层也当作3层来处理)
     */
    
    //测试数据：
    NSArray * items = @[@"节日送礼",@"婚庆用酒",@"名优白酒",@"闺蜜聚会",@"小资生活",@"商务宴请",@"高端派对"];
    
    NSInteger countMax= nameArray.count;
    for (int i=0; i<countMax; i++) {
        
        rightMeun * meun=[[rightMeun alloc] init];
        meun.meunName = nameArray[i];
        NSMutableArray * sub=[NSMutableArray arrayWithCapacity:0];
        for ( int j=0; j <1; j++) {//这里是section的数量
            
            rightMeun * menu1=[[rightMeun alloc] init];
            menu1.urlName = @"http://i3.sinaimg.cn/gm/2013/0424/U5253P115DT20130424162811.jpg";
            
            [sub addObject:menu1];
            NSMutableArray *zList=[NSMutableArray arrayWithCapacity:0];
            for ( int z=0; z <items.count; z++) {
                
                rightMeun * meun2=[[rightMeun alloc] init];
                meun2.meunName= items[z];
                [zList addObject:meun2];
                
            }
            menu1.nextArray=zList;
        }

        meun.nextArray=sub;
        [lis addObject:meun];
    }
    
    /**
     *  适配 ios 7 和ios 8 的 坐标系问题
     */
    self.automaticallyAdjustsScrollViewInsets=NO;
    
    /**
     默认是 选中第一行
     */
    MultilevelMenu * view=[[MultilevelMenu alloc] initWithFrame:CGRectMake(0, 64, SCREEN_WIDTH, SCREEN_HEIGHT-64-44) WithData:lis withSelectIndex:^(NSInteger left, NSInteger right,rightMeun* info) {
        
        NSLog(@"点击的菜单：%@",info.meunName);
    }];
    
    view.needToScorllerIndex=0;
    view.isRecordLastScroll=YES;
    [self.view addSubview:view];
