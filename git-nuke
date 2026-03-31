#!/usr/bin/env bash

warn() { echo -e "${RED}  ⚠${NC} $1"; }

git_nuke() {
  set -e

  local branch current

  branch="${1:-$(git branch --show-current)}"

  if [ -z "$branch" ]; then
    echo "Could not determine branch name."
    return 1
  fi

  case "$branch" in
    main|master|dev|develop|development|stage|staging)
      warn "Refusing to delete protected branch: $branch"
      return 1
      ;;
  esac

  current="$(git branch --show-current)"

  if [ "$current" = "$branch" ]; then
    warn "Cannot delete current branch. Switch to another branch before deleting it."
    return 1
  fi

  if git show-ref --verify --quiet "refs/heads/$branch"; then
    git branch -D "$branch"
  else
    echo "Local branch does not exist: $branch"
  fi

  if git ls-remote --exit-code --heads origin "$branch" >/dev/null 2>&1; then
    git push origin --delete "$branch"
  else
    echo "Remote branch does not exist on origin: $branch"
  fi
}
