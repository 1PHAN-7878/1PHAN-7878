---
title: Unity中的自动寻路Navigation使用
date: 2023-11-16 14:22:48
tags: Unity
---
# 包导入

窗口中选择包管理器，搜索AI，添加相应的包，接下来可以在窗口中选择AI面板，要选择那个过时的使用（泄。


# 场景配置

搭建如图所示的地形

![image-20231116142557278](../images/image-20231116142557278.png)

将不需要移动的设置为静态。

![image-20231116142747375](../images/image-20231116142747375.png)

点击navigation的面板，生成自动寻路网格。

![image-20231116143021803](../images/image-20231116143021803.png)

# 组件配置

选择要添加的物体，添加Nav Mesh Agent。再添加一个C#脚本。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.AI;

public class AI : MonoBehaviour
{
    public GameObject gameObject;
    private NavMeshAgent agent;
    public Transform target; // 设置目标位置
    // Start is called before the first frame update
    void Start()
    {
        //gameObject = GameObject.Find("Tree");
        
        agent = GetComponent<NavMeshAgent>();
        SetDestination();
    }

    // Update is called once per frame
    void Update()
    {
        
    }

    void SetDestination()
    {
        if (target != null)
        {
            agent.SetDestination(target.position);
        }
    }
}

```

# 实现

![image-20231116144928854](../images/image-20231116144928854.png)
