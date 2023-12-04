---
title: Unity中实现摄像头跟随物体旋转移动
date: 2023-12-04 20:47:26
tags: Unity
---

# 需求

想做一个类似于很多游戏中，你移动了视角，摄像机移动了视角，物体移动了角度。但是物体还是保持在屏幕中心，而且当你移动之后，wasd控制的移动是根据你的视角向前移动的，而不是向初始的方向移动，这个其实做起来还是有点难度（新。

# 实现

`player.cs`

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class player : MonoBehaviour
{
    public Camera playerCamera;
    public float rotateSpeed = 3f;
    public float moveSpeed = 1f;

    public Rigidbody rb;
    private int raycastDistance;

    // Start is called before the first frame update
    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
        //// 获取输入
        //float horizontal = Input.GetAxis("Horizontal");
        //float vertical = Input.GetAxis("Vertical");

        //// 获取相机的正前方和正右方向
        //Vector3 cameraForward = Camera.main.transform.forward;
        //Vector3 cameraRight = Camera.main.transform.right;

        //// 计算移动方向

        ////Vector3 movement = new Vector3(horizontal, 0f, vertical) * moveSpeed;
        //Vector3 movement = (cameraForward * vertical + cameraRight * horizontal).normalized;
        ////Vector3 movement = new Vector3(horizontal, 0f, vertical) * moveSpeed;
        //// 应用移动
        ////rb.AddForce(movement, ForceMode.Acceleration);
        //rb.MovePosition(transform.position + movement);
        //// 获取鼠标水平移动的输入
        //float mouseX = Input.GetAxis("Mouse X");

        //// 计算旋转角度
        //float rotationAmount = mouseX * rotateSpeed;

        //// 应用旋转
        //transform.Rotate(Vector3.up, rotationAmount);

        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");

        // 获取摄像机的朝向
        Vector3 cameraForward = playerCamera.transform.forward;
        Vector3 cameraRight = playerCamera.transform.right;

        //cameraForward.y = 0f;
        //cameraRight.y = 0f;
        // 计算移动方向
        //Vector3 movement = new Vector3(horizontal, 0f, vertical) * moveSpeed;
        // 根据输入和摄像机的朝向计算移动方向
        Vector3 movement = (cameraForward.normalized * vertical + cameraRight.normalized * horizontal) * moveSpeed;
        movement.y = 0f;
        // 应用移动
        //rb.AddForce(movement, ForceMode.VelocityChange);
        rb.MovePosition(movement + rb.position);
    }
}

```



`camera.cs`

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class camera : MonoBehaviour
{

    public Transform target;
    public Vector3 offset;  // 相机相对于物体的偏移量
    public Vector3 newPosition;
    public float followSpeed = 5f; // 跟随速度
    public float rotationSpeed = 2f; // 旋转速度

    public float rotateSpeed = 3f;
    // Start is called before the first frame update
    void Start()
    {
        offset = transform.position - target.position;
    }

    // Update is called once per frame
    void Update()
    {
        //newPosition = target.position + offset;
        //transform.position = newPosition;
        //transform.position = Vector3.Lerp(transform.position, newPosition, Time.deltaTime * followSpeed);
        //Vector3 targetDirection = target.position - transform.position;

        // 计算目标旋转角度，并将 y 分量设为 0
        //Quaternion targetRotation = Quaternion.LookRotation(targetDirection, Vector3.up);
        //targetRotation.eulerAngles = new Vector3(targetRotation.eulerAngles.x, 0f, 0f);

        // 使用 Slerp 函数平滑地旋转摄像机
        //transform.rotation = Quaternion.Slerp(transform.rotation, targetRotation, Time.deltaTime * rotationSpeed);


        float mouseX = Input.GetAxis("Mouse X");
        float mouseY = Input.GetAxis("Mouse Y");
        // 计算旋转角度
        float rotationAmountX = mouseX * rotateSpeed;
        //float rotationAmountY = mouseY * rotateSpeed;
        Vector3 rotation = new Vector3(0, rotationAmountX, 0);
        // 围绕目标旋转摄像机
        target.Rotate(rotation);

    }
}

```

# 总结

总体来说是物体作为摄像机的父物体，但传入移动信号时，游戏物体找到摄像机的前后左右，控制方向的移动，而不是摄像机移动。当鼠标控制视角，是摄像机控制了父物体，也就是游戏物体的旋转，因为摄像机是子物体，所以会跟随进行旋转。
