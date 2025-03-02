/*
 * Copyright (C) 2017-2021
 * All rights reserved, Designed By 深圳中科鑫智科技有限公司
 * Copyright authorization contact 18814114118
 */
package com.shop.cereshop.business.controller;

import com.shop.cereshop.business.annotation.NoRepeatSubmit;
import com.shop.cereshop.business.annotation.NoRepeatWebLog;
import com.shop.cereshop.business.param.live.LiveGetAllParam;
import com.shop.cereshop.business.param.live.LiveProductParam;
import com.shop.cereshop.business.param.live.LiveProductGetAllParam;
import com.shop.cereshop.business.param.live.LiveProductParam;
import com.shop.cereshop.business.service.live.CereLiveProductService;
import com.shop.cereshop.business.utils.ContextUtil;
import com.shop.cereshop.commons.domain.business.CerePlatformBusiness;
import com.shop.cereshop.commons.domain.common.Page;
import com.shop.cereshop.commons.domain.live.CereLive;
import com.shop.cereshop.commons.domain.live.CereLiveProduct;
import com.shop.cereshop.commons.exception.CoBusinessException;
import com.shop.cereshop.commons.result.Result;
import com.shop.cereshop.commons.utils.GsonUtil;
import io.swagger.annotations.ApiOperation;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;

import javax.servlet.http.HttpServletRequest;

/**
 * 直播间商品管理
 */
@RestController
@RequestMapping("liveProduct")
/**
 * 注解方式生成日志对象，指定topic生成对象类名
 */
@Slf4j(topic = "LiveProductController")
public class LiveProductController {

    @Autowired
    private CereLiveProductService cereLiveProductService;

    /**
     * 直播间商品列表查询
     * @param param
     * @return
     */
    @PostMapping(value = "getAll")
    @ApiOperation(value = "直播间商品列表查询")
    public Result<Page<CereLiveProduct>> getAll(@RequestBody LiveProductGetAllParam param, HttpServletRequest request) throws CoBusinessException,Exception{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        param.setShopId(user.getShopId());
        Page page= cereLiveProductService.getAll(param);
        return new Result(page);
    }

    /**
     * 添加直播间商品
     * @param param
     * @return
     */
    @PostMapping(value = "save")
    @NoRepeatSubmit
    @ApiOperation(value = "添加直播间商品")
    @NoRepeatWebLog
    public Result save(@RequestBody @Validated LiveProductParam param, HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        param.setShopId(ContextUtil.getShopId());
        cereLiveProductService.save(param,user);
        return new Result(user.getUsername(),"添加直播间商品", GsonUtil.objectToGson(param));
    }

    /**
     * 修改直播间
     * @param param
     * @return
     */
    @PostMapping(value = "update")
    @NoRepeatSubmit
    @ApiOperation(value = "修改直播间")
    @NoRepeatWebLog
    public Result update(@RequestBody LiveProductParam param, HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        param.setShopId(ContextUtil.getShopId());
        cereLiveProductService.update(param,user);
        return new Result(user.getUsername(),"修改直播间", GsonUtil.objectToGson(param));
    }

    /**
     * 删除直播间
     * @param param
     * @return
     */
    @PostMapping(value = "delete")
    @NoRepeatSubmit
    @ApiOperation(value = "删除直播间")
    @NoRepeatWebLog
    public Result delete(@RequestBody LiveProductParam param, HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        cereLiveProductService.delete(param.getId(),user);
        return new Result(user.getUsername(),"删除直播间", GsonUtil.objectToGson(param));
    }

    /**
     * 查询某个直播间商品
     * @param param
     * @return
     */
    @PostMapping(value = "getById")
    @NoRepeatSubmit
    @ApiOperation(value = "查询某个直播间商品")
    @NoRepeatWebLog
    public Result getById(@RequestBody LiveProductParam param, HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        param.setShopId(user.getShopId());
        CereLiveProduct liveProduct = cereLiveProductService.getById(param);
        return new Result(liveProduct);
    }

    /**
     * 重新审核某个直播间商品
     * @param param
     * @return
     */
    @PostMapping(value = "reExamine")
    @NoRepeatSubmit
    @ApiOperation(value = "重新审核某个直播间商品")
    @NoRepeatWebLog
    public Result<Integer> reExamine(@RequestBody LiveProductParam param, HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformBusiness user = (CerePlatformBusiness) request.getAttribute("user");
        param.setShopId(user.getShopId());
        int result = cereLiveProductService.reExamine(param);
        return new Result(result);
    }

}
