---
title: laravel学习-1
date: 2017-04-06 14:49:48
categories: php
tags: []
urlname: 26
---
laravel基础


<!--more-->

<?php

/*
|--------------------------------------------------------------------------
| Routes File
|--------------------------------------------------------------------------
|
| Here is where you will register all of the routes in an application.
| It's a breeze. Simply tell Laravel the URIs it should respond to
| and give it the controller to call when that URI is requested.
|
*/

Route::get('/', function () {
    return view('welcome');
});
//基础路由
Route::get('basic1',function(){
    return 'helloworld';
});
Route::post('basic2',function(){
    return 'basic2';
});
//多请求路由
Route::match(['get','post'],'multy1',function(){
    return 'multy1';
});
Route::any('multy2',function (){
    return 'multy2';
});
//路由参数
/*Route::get('user/{ke?}',function($ke=null){
    return $ke;
});*/
/*Route::get('user/{id?}',function($id){
    return $id;
})->where('id','[A-Za-z]+');*/

//Route::get('user/{id?}/{name?}',function($id,$name ='ke'){
//    return $name.$id;
//})->where(['id' => '[0-9]+' ,'name' => '[A-Za-z]+']);

//路由别名
//Route::get('user/11center',['as'=> 'center' , function() {
//    return route('center');
//}]);

//路由群组
//Route::group(['prefix'=>'member'],function (){
//
//    Route::get('user/center',['as'=>'center',function(){
//        return route('center');
//    }]);
//    Route::any('multy2',function (){
//        return 'member-multy2';
//    });
//});


//路由视图
Route::get('view',function (){
    return view('welcome');
});

//Route::get('member/info','MemberController@info');
//Route::match(['get'],'member/info',[
//    'uses'=>'MemberController@info',
//    'as'=>'memberinfo'
//]);

route::any('/member/{id}','MemberController@info')
->where('id','[0-9]+');//注意ID是大括号
/*
|--------------------------------------------------------------------------
| Application Routes
|--------------------------------------------------------------------------
|
| This route group applies the "web" middleware group to every route
| it contains. The "web" middleware group is defined in your HTTP
| kernel and includes session state, CSRF protection, and more.
|
*/

Route::group(['middleware' => ['web']], function () {
    //
});
