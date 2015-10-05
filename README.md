# RestController
Controller
package com.publishing.controller;

import java.util.Date;
import java.util.List;

import org.apache.log4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;

import com.publishing.model.Article;
import com.publishing.model.Status;
import com.publishing.services.DataServices;

@Controller
@RequestMapping("/article")
public class RestController {

	@Autowired
	DataServices dataServices;

	static final Logger logger = Logger.getLogger(RestController.class);

	@RequestMapping(value = "/create", method = RequestMethod.POST, consumes = MediaType.APPLICATION_JSON_VALUE)
	public @ResponseBody
	Status addArticle(@RequestBody Article article) {
		try {
			dataServices.addEntity(article);
			return new Status(1, "Article added Successfully !");
		} catch (Exception e) {
			// e.printStackTrace();
			return new Status(0, e.toString());
		}

	}

	@RequestMapping(value = "/update", method = RequestMethod.POST, consumes = MediaType.APPLICATION_JSON_VALUE)
	public @ResponseBody
	Status updateArticle(@RequestBody Article article) {
		try {
			dataServices.updateEntity(article);
			return new Status(1, "Article added Successfully !");
		} catch (Exception e) {
			// e.printStackTrace();
			return new Status(0, e.toString());
		}

	}

	@RequestMapping(value = "delete/{id}", method = RequestMethod.GET)
	public @ResponseBody
	Status deleteArticle(@PathVariable("id") long id) {

		try {
			dataServices.deleteEntity(id);
			return new Status(1, "Article deleted Successfully !");
		} catch (Exception e) {
			return new Status(0, e.toString());
		}

	}

	@RequestMapping(value = "/{id}", method = RequestMethod.GET)
	public @ResponseBody
	Article getArticle(@PathVariable("id") long id) {
		Article article = null;
		try {
			article = dataServices.getEntityById(id);

		} catch (Exception e) {
			e.printStackTrace();
		}
		return article;
	}

	@RequestMapping(value = "/list", method = RequestMethod.GET)
	public @ResponseBody
	List<Article> getArticle() {

		List<Article> articleList = null;
		try {
			articleList = dataServices.getEntityList();

		} catch (Exception e) {
			e.printStackTrace();
		}

		return articleList;
	}
	
	@RequestMapping(value = "/{author}", method = RequestMethod.GET)
	public @ResponseBody
	List<Article> getArticleByAuthor(@PathVariable("author") String author) {
		List<Article> articles = null;
		try {
			articles = dataServices.getEntityListByAuthor(author);

		} catch (Exception e) {
			e.printStackTrace();
		}
		return articles;
	}

	@RequestMapping(value = "/{keyword}", method = RequestMethod.GET)
	public @ResponseBody
	List<Article> getArticleByKeyword(@PathVariable("keyword") String keyword) {
		List<Article> articles = null;
		try {
			articles = dataServices.getEntityListByKeyword(keyword);

		} catch (Exception e) {
			e.printStackTrace();
		}
		return articles;
	}

	@RequestMapping(value = "/dates/from/{fromdate}/to/{todate}", method = RequestMethod.GET)
	public @ResponseBody
	List<Article> getArticleByDateRange(@PathVariable("fromdate") long fromDate, @PathVariable("todate") long toDate) {
		List<Article> articles = null;
		try {
			articles = dataServices.getEntityListByDateRange(new Date(fromDate), new Date(toDate));

		} catch (Exception e) {
			e.printStackTrace();
		}
		return articles;
	}


}
/Comment/
