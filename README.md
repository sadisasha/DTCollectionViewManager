![Build Status](https://travis-ci.org/DenHeadless/DTCollectionViewManager.png?branch=master,development)

DTCollectionViewManager
=======================

> This is a sister-project for [DTTableViewManager](https://github.com/DenHeadless/DTTableViewManager) - great tool for UITableView management, built on the same principles.

## Features

* Powerful and clean mapping system between data models and UICollectionView cells, supplementary views 
* Automatic datasource and interface synchronization
* Dramatic decrease of code amount needed for UICollectionView implementation
* Good unit test coverage

## Requirements

- iOS 6,7
- ARC

## Workflow

Here are 4 simple steps you need to use DTCollectionViewManager:

1. Your view controller should subclass DTCollectionViewController, and set collectionView, delegate and datasource properties to self.
2. You should have subclasses of UICollectionViewCell, that implement DTCollectionViewModelTransfer protocol.
3. In your viewDidLoad method, call mapping methods to establish relationship between data models and UICollectionViewCells.
4. Add your data models!

## Mapping

Every mapping method will automatically check for existance of xib with the same name. If it does exist - nib will be registered for creating cells. If not - class will be registered. When collection view will need to present content, cells will be created using dequeueReusableCellWithReuseIdentifier:forIndexPath: method. Then every cell will get called with updateWithModel: method, passing data model to cell, so it could present it's data.

Mapping cells:

```objective-c
[self registerCellClass:[Cell class] forModelClass:[Model class]];
```

Mapping supplementary views:
```objective-c
[self registerSupplementaryClass:[SupplementaryClass class] forKind:UICollectionElementKindSectionHeader
                   forModelClass:[Model class]]
```

## Managing collection items

##### Adding items

```objective-c
[self addCollectionItem:model];
[self addCollectionItem:model toSection:1];
[self addCollectionItems:@[model1,model2]];
[self addCollectionItems:@[model1,model2] toSection:0];
```

##### Removing items

```objective-c
[self removeCollectionItem:model];
[self removeCollectionItemAtIndexPath:indexPath];
[self removeCollectionItems:@[model1,model2]];
[self removeCollectionItemsAtIndexPaths:@[index1,index2]];
[self removeAllCollectionItems];
```	

#### Move, insert, replace

```objective-c
[self insertItem:model atIndexPath:indexPath];
[self moveItem:model toIndexPath:indexPath];
[self replaceItem:model withItem:newModel];
```

#### Managing sections

```objective-c
[self moveSection:fromSection toSection:toSection];
[self deleteSections:indexSet];
```	

#### Search 

```objective-c
[self numberOfSections];
[self numberOfCollectionItemsInSection:2];
[self collectionItemAtIndexPath:indexPath];
```	

## Installation

Simplest option is to use [CocoaPods](http://www.cocoapods.org):

	pod 'DTCollectionViewManager', '~> 1.0.0'
	
## Documentation

[Cocoadocs](http://cocoadocs.org/docsets/DTCollectionViewManager)

## Example

Take a look at Example folder in repo.

## iOS 6 Notes

UICollectionView has some severe bugs in iOS 6. The most annoying of them is assert for global index path, which happens, when you insert first item in a section, or section without items, etc. It is tracked on [OpenRadar](http://openradar.appspot.com/12954582), however it doesn't seem it will get fixed on iOS 6. So DTCollectionViewManager has some iOS 6-specific workarounds to prevent crashes. However, to implement them, i had to tweak collection view behaviour, and change some animations. And workarounds are not bullet-proof.

iOS 7 fixes all of this mess, and everything should work perfectly there. 

## Roadmap

- Search in UICollectionView

